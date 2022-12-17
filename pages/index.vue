<template>
  <div class="text-xl">
    <!-- thông báo -->

    <div
      v-if="open"
      class="toast toast-center toast-middle card w-96 bg-base-100 shadow-xl z-50"
    >
      <div class="card-body">
        <h2 class="card-title">Thông báo cực căng ?!</h2>
        <p>{{ messageDialog }}</p>
        <div class="card-actions justify-end">
          <button @click="open = false" class="btn btn-primary">Okey!!</button>
        </div>
      </div>
    </div>
    <div class="z-0" :class="[open ? 'blur-lg' : '']">
      <!-- chọn ban -->
      <div class="mx-auto w-4/5 m-5">
        <select
          v-model="selectTeam1"
          class="text-xl select select-primary w-full max-w-xs"
        >
          <option value=" " disabled selected>Chọn ban của bạn</option>
          <option :value="team.id" v-for="team in teams" :key="team.id">
            {{ team.name }}
          </option>
        </select>
      </div>

      <!-- chọn tên -->
      <div v-show="selectTeam1 == ' '" class="mx-auto w-4/5 m-5">
        <select disabled class="text-xl select select-primary w-full max-w-xs">
          <option disabled selected>Chọn tên của bạn</option>
        </select>
      </div>

      <div v-show="selectTeam1 != ' '" class="mx-auto w-4/5 m-5">
        <select
          v-model="selectUser1"
          class="text-xl select select-primary w-full max-w-xs"
        >
          <option value=" " disabled selected>Chọn ban của bạn</option>
          <option :value="user.id" v-for="user in listUser1" :key="user.name">
            {{ user.name }}
          </option>
        </select>
      </div>

      <!-- chọn các tùy chọn  -->
      <div v-for="data in dataSelect" :key="data.title">
        <!-- xe 100cc -->
        <div class="mx-auto w-4/5 m-5 ring rounded-2xl p-5">
          <div class="font-medium m-1">{{ data.title }}</div>
          <div class="form-control">
            <label class="label cursor-pointer">
              <span class="label-text text-xl">{{ data.value1 }}</span>
              <input
                value="1"
                v-model="data.selectValue"
                type="radio"
                :name="data.title"
                class="radio checked:bg-red-500"
              />
            </label>
          </div>
          <div class="form-control">
            <label class="label cursor-pointer">
              <span class="label-text text-xl">{{ data.value2 }}</span>
              <input
                value="2"
                v-model="data.selectValue"
                type="radio"
                :name="data.title"
                class="radio checked:bg-blue-500"
              />
            </label>
          </div>
        </div>
      </div>
      <div class="mx-auto w-4/5 m-5 font-medium"></div>

      <!-- chọn ban muốn di cùng -->
      <transition name="bounce">
        <div v-if="dataSelect[5].selectValue == 1">
          <div class="mx-auto w-4/5 m-5">
            <select
              v-model="selectTeam2"
              class="text-xl select select-primary w-full max-w-xs"
            >
              <option value=" " disabled selected>
                Chọn ban của người đi chung với bạn
              </option>
              <option :value="team.id" v-for="team in teams" :key="team.id">
                {{ team.name }}
              </option>
            </select>
          </div>

          <!-- chọn tên -->
          <div v-show="selectTeam2 == ' '" class="mx-auto w-4/5 m-5">
            <select disabled class="text-xl select select-primary w-full max-w-xs">
              <option disabled selected>Chọn tên của người đi chung với bạn</option>
            </select>
          </div>

          <div v-show="selectTeam2 != ' '" class="mx-auto w-4/5 m-5">
            <select
              v-model="selectUser2"
              class="text-xl select select-primary w-full max-w-xs"
            >
              <option value=" " disabled selected>
                Chọn tên của người đi chung với bạn
              </option>
              <option :value="user.id" v-for="user in listUser2" :key="user.name">
                {{ user.name }}
              </option>
            </select>
          </div>
        </div>
      </transition>

      <div class="text-center m-5">
        <div @click="dk()" :class="[loading ? 'loading' : '']" class="btn btn-primary">
          đăng kí sắp xe
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const selectTeam1 = ref(" ");
const selectTeam2 = ref(" ");
const selectUser1 = ref(" ");
const selectUser2 = ref(" ");
const loading = ref(false);
const messageDialog = ref();
const open = ref(false);
// const url = "http://localhost:8088";
const url = "https://api-websepxe.vercel.app";

const { data: teams } = await useFetch(`${url}/api/team`);
const { data: users } = await useFetch(`${url}/api/users`);
const { data: times } = await useFetch(`${url}/api/time`);

const listUser1 = computed(() => {
  if (selectTeam1 != " ") {
    return users.value.filter((user) => user.team == selectTeam1.value);
  }
  return [];
});

const listUser2 = computed(() => {
  if (selectTeam2 != " ") {
    return users.value.filter((user) => user.team == selectTeam2.value);
  }
  return [];
});
const dataSelect = ref([
  {
    title: "Bạn có xe 100cc không?",
    value1: "Có",
    value2: "Không",
    selectValue: "",
  },
  {
    title: "Tay lái bạn có tốt không?",
    value1: "Có",
    value2: "Không",
    selectValue: "",
  },
  {
    title: "Bạn có bằng lái không",
    value1: "Có",
    value2: "Không",
    selectValue: "",
  },
  {
    title: "Thời gian nhập đoàn là",
    value1: times.value[0].name,
    value2: times.value[1].name,
    selectValue: "",
  },
  {
    title: "Thời gian xuất đoàn là",
    value1: times.value[0].name,
    value2: times.value[1].name,
    selectValue: "",
  },
  {
    title:
      "Bạn có nguyện vọng muốn chở ai đó hoặc đưa tấm thân mình cho đồng đội nào không ?",
    value1: "Có",
    value2: "Không",
    selectValue: "",
  },
]);

function selectAll() {
  if (selectUser1.value) {
    let mark = 1;
    dataSelect.value.forEach((e) => {
      if (!e.selectValue) {
        mark = 0;
        return;
      }
    });
    return mark;
  }
  return 0;
}

function openDialog(message) {
  open.value = true;
  messageDialog.value = message;
}

async function dk() {
  loading.value = true;
  try {
    if (selectAll()) {
      let data = {
        xe: dataSelect.value[0].selectValue,
        taylai:
          dataSelect.value[1].selectValue && dataSelect.value[2].selectValue ? 1 : 2,
        time_di: times.value[dataSelect.value[3].selectValue - 1].id,
        time_ve: times.value[dataSelect.value[3].selectValue - 1].id,
      };
      if (selectUser2.value != " ") {
        data.want = selectUser2.value;
      }
      const { data: document, error } = await useFetch(
        `${url}/api/users/${selectUser1.value}`,
        {
          headers: {
            "Content-Type": "application/json",
            Accept: "application/json",
          },
          method: "put",
          body: data,
        }
      );
      if (!error.value) {
        useRouter().push("/thanhcong");
      } else {
        openDialog(
          "có 1 thế lực nào đó làm bạn đăng kí không được, bạn hãy quay lại sau nhé!!!"
        );
      }
    } else {
      openDialog("Bạn cần phải nhập đầy đủ các thông tin!!!");
    }
    return;
  } catch (error) {
    console.log("lỗi dk");
    console.log(error);
  } finally {
    loading.value = false;
  }
}
</script>

<style scoped>
.bounce-enter-active {
  animation: bounce-in 0.5s;
}
.bounce-leave-active {
  animation: bounce-in 0.5s reverse;
}
@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  /* 25% {
    transform: scale(0.25);
  } */
  50% {
    transform: scale(2);
  }
  /* 75% {
    transform: scale(0.75);
  } */
  100% {
    transform: scale(1);
  }
}
</style>

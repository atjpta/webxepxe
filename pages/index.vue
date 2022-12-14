<template>
  <div>
    <header>
      <h1 class="font-bold">SẮP XE XUÂN YÊU THƯƠNG 2022</h1>
    </header>

    <!-- chọn ban -->
    <div class="mx-auto w-4/5 m-5">
      <select class="select select-primary w-full max-w-xs">
        <option disabled selected>Chọn ban của bạn</option>
        <option>Game of Thrones</option>
        <option>Lost</option>
        <option>Breaking Bad</option>
        <option>Walking Dead</option>
      </select>
    </div>

    <!-- chọn tên -->
    <div class="mx-auto w-4/5 m-5">
      <select class="select select-primary w-full max-w-xs">
        <option disabled selected>Chọn tên của bạn</option>
        <option>Game of Thrones</option>
        <option>Lost</option>
        <option>Breaking Bad</option>
        <option>Walking Dead</option>
      </select>
    </div>
    <!-- chọn các tùy chọn  -->
    <div v-for="data in dataSelect" :key="data.title">
      <!-- xe 100cc -->
      <div class="mx-auto w-4/5 m-5 ring rounded-2xl p-5">
        <div class="font-medium m-1">{{ data.title }}</div>
        <div class="form-control">
          <label class="label cursor-pointer">
            <span class="label-text">{{ data.value1 }}</span>
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
            <span class="label-text">{{ data.value2 }}</span>
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
          <select class="select select-primary w-full max-w-xs">
            <option disabled selected>Chọn ban của người đi chung với bạn</option>
            <option>Game of Thrones</option>
            <option>Lost</option>
            <option>Breaking Bad</option>
            <option>Walking Dead</option>
          </select>
        </div>

        <!-- chọn tên -->
        <div class="mx-auto w-4/5 m-5">
          <select class="select select-primary w-full max-w-xs">
            <option disabled selected>Chọn tên người đi chung với bạn</option>
            <option>Game of Thrones</option>
            <option>Lost</option>
            <option>Breaking Bad</option>
            <option>Walking Dead</option>
          </select>
        </div>
      </div>
    </transition>

    <div class="text-center m-5">
      <div class="btn btn-primary">đăng kí sắp xe</div>
    </div>
    {{ users }}
  </div>
</template>

<script setup>
const url = "http://localhost:8088";
const users = await useFetch(`${url}/api/users`);

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
    value1: "5h30",
    value2: "11h30",
    selectValue: "",
  },
  {
    title: "Thời gian xuất đoàn là",
    value1: "5h30",
    value2: "11h30",
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
</script>

<style scoped>
header {
  background-image: url("../asset/image/317641038_6374923505855862_4793296601509338930_n.jpg");
}
header H1 {
  font-size: 60px;
  text-align: center;
  color: yellow;
  text-shadow: 0.1em 0.1em #333;
  font-family: "Times New Roman", Times, serif;
}

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

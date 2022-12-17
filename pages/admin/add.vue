<template>
  <div>
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
      <div class="text-4xl text-center">Thêm người dùng</div>
      <div class="ring-2 p-5 m-5 w-3/5 mx-auto rounded-md">
        <div class="m-5">
          <div class="text-2xl mb-2">tên người dùng</div>
          <input
            v-model="nameUser"
            class="bg-white/5 border-0 border-b-2 border-primary text-xl mb-5 p-2 w-full"
            type="text"
          />
        </div>
        <div class="m-5">
          <div class="text-2xl mb-2">chọn ban của người dùng</div>
          <select
            v-model="selectTeam"
            class="select select-primary w-full max-w-xs text-xl"
          >
            <option value=" " disabled selected>Chọn ban</option>
            <option :value="team.id" v-for="team in teams" :key="team.id">
              {{ team.name }}
            </option>
          </select>
        </div>
        <!-- btn -->
        <div class="text-center">
          <div
            @click="add()"
            :class="[loading ? 'loading' : '']"
            class="btn btn-primary btn-outline"
          >
            thêm
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
definePageMeta({
  layout: "menudashboard",
});
const open = ref(false);
const selectTeam = ref(" ");
const loading = ref(false);
const messageDialog = ref();
const nameUser = ref();
// const url = "http://localhost:8088";
const url = "https://api-websepxe.vercel.app";
const { data: teams } = await useFetch(`${url}/api/team`);

function openDialog(message) {
  open.value = true;
  messageDialog.value = message;
}

async function add() {
  loading.value = true;
  try {
    console.log(selectTeam.value);
    if (selectTeam.value != " " && nameUser.value.length > 0) {
      const { data: document, error } = await useFetch(`${url}/api/users`, {
        headers: {
          "Content-Type": "application/json",
          Accept: "application/json",
        },
        method: "post",
        body: {
          name: nameUser.value,
          team: selectTeam.value,
        },
      });
      if (!error.value) {
        openDialog("bạn đã thêm thành công");
        selectTeam.value = " ";
        nameUser.value = "";
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

<style></style>

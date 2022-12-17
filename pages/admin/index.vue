<template>
  <div class="">
    <div class="text-3xl text-center uppercase mb-5">danh sách user</div>

    <div class="text-right m-5">
      <nuxt-link to="/admin/add">
        <div class="btn btn-primary btn-outline">
          <icon class-icon="mr-2 text-2xl" icon="fa-solid fa-circle-plus" />
          thêm người dùng
        </div>
      </nuxt-link>
    </div>

    <div class="bg-base-200 p-5 rounded-2xl w-full">
      <div>
        <div class="btn-group justify-center flex">
          <button @click="nextList(-1)" :class="[loading ? 'loading' : '']" class="btn">
            «
          </button>
          <button class="btn">Trang {{ page + 1 }}</button>
          <button @click="nextList(+1)" :class="[loading ? 'loading' : '']" class="btn">
            »
          </button>
        </div>
        <div class="bg-base-300 rounded-2xl ring-1 flex justify-around space-x-5 m-5 p-5">
          <div v-for="title in titletable" :key="title">
            <div class="divider divider-horizontal"></div>
            <div class="w-20">{{ title }}</div>
          </div>
        </div>
      </div>
      <div v-for="(user, index) in listUsers" :key="user.id">
        <v-mono-user
          :addClass="
            index % 2 == 0
              ? 'ring-info hover:bg-info/20'
              : 'ring-primary hover:bg-primary/20'
          "
          :data="user"
        />
      </div>
      <div class="btn-group justify-center flex">
        <button @click="nextList(-1)" :class="[loading ? 'loading' : '']" class="btn">
          «
        </button>
        <button class="btn">Trang {{ page + 1 }}</button>
        <button @click="nextList(1)" :class="[loading ? 'loading' : '']" class="btn">
          »
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
definePageMeta({
  layout: "menudashboard",
});
const loading = ref(false);
// const url = "http://localhost:8088";
const url = "https://api-websepxe.vercel.app";
const listUsers = ref();
const page = ref(0);
const { data: maxpage } = await useFetch(`${url}/api/users/max/page`);
const { data: users } = await useFetch(`${url}/api/users/${page.value}`);
listUsers.value = users.value;
maxpage.value = parseInt(maxpage.value);
async function nextList(value) {
  try {
    loading.value = true;
    page.value += value;
    if (page.value < 0) {
      page.value = maxpage.value;
    }
    if (page.value > maxpage.value) {
      page.value = 0;
    }
    const { data: users } = await useFetch(`${url}/api/users/${page.value}`);
    listUsers.value = users.value;
  } catch (error) {
    console.log(error);
    console.log("lỗi chuyển trang");
  } finally {
    loading.value = false;
  }
}

const titletable = ref([
  "Tên",
  "Xe",
  "Có thể lái",
  "Ban",
  "Thời gian đi",
  "Thời gian về",
  "Muốn đi với",
  "kết quả ghép",
  "tùy chọn",
]);
</script>

<style></style>

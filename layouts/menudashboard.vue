<template>
  <div>
    <defaultVue />
    <v-menu />
    <!-- nọi dung trang -->
    <div class="sm:flex">
      <div class="sm:w-80"></div>
      <div class="w-full px-10">
        <slot />
      </div>
    </div>
  </div>
</template>

<script setup>
import defaultVue from "./default.vue";

const hidenMenu = ref(false);

const router = useRouter();
const route = useRoute();
const data = ref([
  {
    title: "danh sách người dùng",
    url: "admin/user",
    icon: "fa-solid fa-users",
  },
  {
    title: "thêm người dùng",
    url: "admin/user/add",
    icon: "fa-solid fa-user-plus",
  },
  {
    title: "sửa người dùng",
    url: "admin/user/edit",
    icon: "fa-solid fa-user-pen",
  },
]);
const open = ref("admin/user");
const link = route.fullPath;
let url = link.substring(11, link.length);
let mark = false;

data.value.forEach((e) => {
  if (e.url == url) {
    mark = true;
    open.value = e.title;
    return;
  }
  if (mark) {
    return;
  }
});
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

.router-link-exact-active {
  color: white;
  background: teal;
}
</style>

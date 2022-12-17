<template>
  <div>
    <div class="">
      <!-- content page -->
      <div class="">
        <!-- menu -->

        <div>
          <div class="dropdown sm:dropdown-open">
            <transition name="bounce">
              <div>
                <div
                  tabindex="0"
                  class="dropdown-content menu p-2 shadow bg-base-200 rounded-box m-5"
                >
                  <div class="btn no-animation btn-ghost my-10 btn-lg">
                    Dashboard Admin
                  </div>
                  <ul class="menu w-64 p-2 rounded-box">
                    <div v-for="i in data" :key="i.title">
                      <li class="menu-title text-base text-start">
                        <NuxtLink class="text-base btn btn-ghost" :to="`/${i.url}`">
                          <Icon classIcon="mr-3" :icon="i.icon" />
                          {{ i.title }}
                        </NuxtLink>
                      </li>

                      <div class="divider"></div>
                    </div>
                  </ul>
                </div>
              </div>
            </transition>
            <transition name="bounce">
              <label
                tabindex="0"
                class="btn btn-primary btn-outline indicator-item indicator-top indicator-end mx-5 mt-5"
              >
                <Icon icon="fa-solid fa-bars" />
              </label>
            </transition>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const hidenMenu = ref(false);

const router = useRouter();
const route = useRoute();
const data = ref([
  {
    title: "danh sách người dùng",
    url: "admin",
    icon: "fa-solid fa-users",
  },
  {
    title: "thêm người dùng",
    url: "admin/add",
    icon: "fa-solid fa-user-plus",
  },
  {
    title: "sửa người dùng",
    url: "admin/edit",
    icon: "fa-solid fa-user-pen",
  },
]);
const open = ref("admin");
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

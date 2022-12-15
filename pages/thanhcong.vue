<template>
  <div>
    <h1 class="font-bold">chúc mừng bạn đã đăng kí thành công</h1>
  </div>
</template>

<script></script>

<style scoped>
div {
  background-image: url("../asset/image/317641038_6374923505855862_4793296601509338930_n.jpg");
}
div H1 {
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

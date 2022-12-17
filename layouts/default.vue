<template>
  <div>
    <header>
      <h1 class="font-bold">SẮP XE XUÂN YÊU THƯƠNG 2022</h1>
    </header>
    <div>
      <slot />
    </div>
  </div>
</template>

<script>
export default {};
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
</style>

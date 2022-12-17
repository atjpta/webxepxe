<template>
  <div>
    <div
      :class="addClass"
      class="rounded-2xl ring-1 flex justify-around space-x-5 m-5 p-5"
    >
      <div class="w-20">{{ data.name }}</div>
      <div class="divider divider-horizontal"></div>

      <div class="w-20">
        {{ data.xe == 2 ? "không có xe" : "có xe" || "chưa điền" }}
      </div>
      <div class="divider divider-horizontal"></div>

      <div class="w-20">
        {{ data.taylai == 2 ? "không thể lái" : "có thể lái" || "chưa điền" }}
      </div>
      <div class="divider divider-horizontal"></div>

      <div class="w-20">{{ data.team.name }}</div>
      <div class="divider divider-horizontal"></div>

      <div class="w-20">
        {{ data.time_di ? data.time_di.name : "chưa điền" }}
      </div>
      <div class="divider divider-horizontal"></div>

      <div class="w-20">{{ data.time_ve ? data.time_ve.name : "chưa điền" }}</div>
      <div class="divider divider-horizontal"></div>

      <div class="w-20">{{ data.want ? data.ban.name : "chưa điền" }}</div>
      <div class="divider divider-horizontal"></div>

      <div class="w-20">{{ data.follow ? data.follow.name : "chưa ghép" }}</div>
      <div class="divider divider-horizontal"></div>

      <div class="btn btn-primary btn-outline btn-xs">
        <Icon icon="fa-solid fa-pen-to-square" />
      </div>
      <div class="btn btn-primary btn-outline btn-xs">
        <Icon icon="fa-solid fa-trash" />
      </div>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  data: Object,
  addClass: String,
});
</script>
<style></style>

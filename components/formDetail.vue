<template>
  <div class="w-36 flex flex-col gap-1 border-2 rounded-lg p-4">
    <img src="" alt="" class="" />
    <p class="mx-auto text-sm text-center h-[30px] container truncate"></p>
    <div class="w-full flex flex-col gap-1">
      <div class="w-full flex gap-1">
        <nuxt-link
          class="w-full border rounded-lg text-white font-medium py-1 text-center bg-green-600"
          >Edit</nuxt-link
        >
        <nuxt-link
          class="w-full border rounded-lg text-white font-medium py-1 text-center bg-green-600"
          >View</nuxt-link
        >
      </div>
      <nuxt-link
        class="w-full border rounded-lg text-white font-medium py-1 text-center bg-blue-600"
        >Download</nuxt-link
      >
    </div>
  </div>
</template>

<script setup></script>

<style scoped></style>

<script setup></script>
<template>
  <div class="w-full h-screen flex items-center justify-center gap-8">
    <div>
      <NuxtLink
        class="bg-green-600 p-4 rounded-lg text-lg font-medium text-white mr-8"
        to="/form/build-form"
      >
        Create new form
      </NuxtLink>
      <NuxtLink
        class="bg-blue-600 p-4 rounded-lg text-lg font-medium text-white"
        to="/form/form-list"
      >
        View froms
      </NuxtLink>
    </div>
  </div>
</template>

<script setup>
import { getData } from "nuxt-storage/local-storage";
import { FileUp } from "lucide-vue-next";

const uploadedFile = ref(null);
const form = getData("form");

function onFileChange(e) {
  uploadedFile.value = e.target.files[0];
}
</script>

<template>
  <div class="w-full bg-slate-200 min-h-screen pb-24">
    <div class="w-[750px] mx-auto" v-if="form">
      <h1 @click="callFile" class="w-full bg-transparent text-2xl py-12">
        {{ form?.formTitle }}
      </h1>
      <ul>
        <li
          v-if="form.formQuestions.length"
          v-for="q in form.formQuestions"
          :key="q"
          class="flex flex-col justify-center bg-white w-full p-10 rounded-lg mb-4"
        >
          <div>
            <div class="flex gap-2 items-start">
              <p class="text-gray-500 text-sm pt-[5.45px]">
                {{ form.formQuestions.indexOf(q) + 1 }}.
              </p>
              <div class="flex w-full text-lg flex-col justify-start gap-2 p-0">
                <p>{{ q.title }}</p>
                <p v-if="q.description" class="text-gray-500 text-sm">
                  {{ q.description }}
                </p>
                <div class="flex items-center gap-2">
                  <label
                    v-if="q.field.type === 'file'"
                    class="w-full hover:cursor-pointer"
                  >
                    <div class="flex items-center gap-2">
                      <FileUp class="h-[40px]" />
                      Upload file

                      <input type="file" ref="upload" @change="onFileChange" />
                    </div>
                    <p class="text-black text-sm mt-4">
                      {{ uploadedFile?.name }}
                    </p>
                  </label>
                  <input
                    v-if="q.field.type === 'text'"
                    class="w-full bg-slate-200 border-2 border-gray-300 rounded-lg h-[60px] p-5"
                  />

                  <div
                    v-if="
                      q.field.type === 'checkbox' || q.field.type === 'radio'
                    "
                    class="flex flex-col gap-2"
                  >
                    <div
                      class=""
                      v-for="option in q.field.options"
                      :key="option"
                    >
                      <label
                        class="w-full bg-transparent flex items-center gap-2"
                      >
                        <input
                          :type="q.field.type"
                          class="bg-slate-200 hover:cursor-pointer bg-transparent border-2 border-gray-300 rounded-lg h-[40px] p-5"
                          name="option"
                        />
                        {{ option.option }}
                      </label>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </li>
      </ul>
      <div class="flex items-center justify-between">
        <button class="w-[250px] bg-blue-600 p-2 border rounded-lg text-white">
          Submit
        </button>
      </div>
    </div>
    <NuxtLayout v-else>
      <div class="">
        <h1 class="text-3xl font-medium">You do not have any form</h1>
      </div>
    </NuxtLayout>
  </div>
</template>

<style scoped>
input {
  outline: none;
}
input[type="file"] {
  display: none;
}
</style>

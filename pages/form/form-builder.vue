<script setup>
import { VueDraggable } from "vue-draggable-plus";
import { setData } from "nuxt-storage/local-storage";
import { ArrowDown, FileUp, Plus, Trash, LucideMove } from "lucide-vue-next";

const formName = ref("");
const questions = ref([]);
const index = ref(0);
const questionKey = ref("");
const questionState = ref(new Map());
const showHelper = ref(false);
const helper = ref(null);
const boolean = ref(true);

function addQuestion() {
  index.value = index.value + 1;
  questionKey.value = "question" + index.value;
  questions.value.push({
    questionKey: questionKey.value,
    title: "",
    field: {
      type: "text",
      options: [
        {
          option: "",
        },
      ],
    },
    required: false,
    description: "",
  });

  questionState.value.set(questionKey.value, {
    showTypeBtn: false,
  });
}

function deleteQuestion(i) {
  questions.value.splice(i, 1);
}

function setType(key, e) {
  showHelper.value = false;
  questionState.value.get(key).showTypeBtn = false;
  questions.value.find((q) => q.questionKey === key).field.type =
    e.target.innerText;
}

function addOption(key) {
  questions.value
    .find((q) => q.questionKey === key)
    .field.options.push({ option: "" });
}

function deleteOption(key, option) {
  const q = questions.value.find((q) => q.questionKey === key);
  q.field.options.splice(q.field.options.indexOf(option), 1);
}

function showFieldType(key) {
  console.log(questions.value);
  showHelper.value = true;
  helper.value.style.height = `${document.body.clientHeight}px`;

  questionState.value.get(key).showTypeBtn =
    !questionState.value.get(key).showTypeBtn;
}

function saveForm() {
  const formTitle = formName.value;
  const formQuestions = questions.value;
  const form = { formTitle: formTitle, formQuestions };
  setData("form", form);

  navigateTo("/form");
}

function helperFunction() {
  questionState.value.forEach((q) => (q.showTypeBtn = false));
  showHelper.value = false;
}
</script>

<template>
  <div class="w-full bg-slate-200 min-h-screen pb-24">
    <div class="w-[750px] mx-auto">
      <h1>
        <input
          type="text"
          class="w-full bg-transparent text-2xl my-12 placeholder:text-black"
          placeholder="Form Name"
          v-model="formName"
        />
      </h1>
      <ul>
        <VueDraggable
          v-if="questions.length"
          :disabled="boolean"
          v-model="questions"
        >
          <li
            v-if="questions.length"
            v-for="q in questions"
            :key="q"
            class="flex flex-col justify-center bg-white w-full p-10 rounded-lg mb-4"
          >
            <button
              class="cursor-move"
              @mouseenter="boolean = false"
              @mouseleave="boolean = true"
            >
              <LucideMove class="w-fit m-auto" />
            </button>
            <div>
              <div class="flex gap-2 items-start">
                <p class="text-gray-500 text-sm pt-[5.45px]">
                  {{ questions.indexOf(q) + 1 }}.
                </p>
                <div
                  class="flex w-full text-lg flex-col justify-start gap-2 p-0"
                >
                  <input
                    class="w-full bg-transparent placeholder:text-black"
                    type="text"
                    v-model="q.title"
                    placeholder="Title"
                  />
                  <input
                    type="text"
                    v-model="q.description"
                    placeholder="Description(optional)"
                    class="w-full bg-transparent"
                  />
                  <div class="flex items-center gap-2">
                    <label
                      v-if="q.field.type === 'file'"
                      class="w-full flex gap-4 items-center hover:cursor-pointer"
                    >
                      <FileUp class="h-[40px]" />
                      Upload file

                      <input type="file" disabled />
                    </label>
                    <input
                      v-if="q.field.type === 'text'"
                      v-model="q.field.content"
                      disabled
                      class="w-full bg-slate-200 border-2 border-gray-300 rounded-lg h-[60px] p-5"
                    />

                    <div
                      v-if="
                        q.field.type === 'checkbox' || q.field.type === 'radio'
                      "
                      class="flex flex-col gap-2"
                    >
                      <div
                        class="flex items-center gap-2"
                        v-for="option in q.field.options"
                        :key="option"
                      >
                        <input
                          :type="q.field.type"
                          class="bg-slate-200 hover:cursor-pointer bg-transparent border-2 border-gray-300 rounded-lg h-[40px] p-5"
                          name="option"
                        />
                        <input
                          type="text"
                          v-model="option.option"
                          class="w-full bg-transparent"
                          placeholder="Option"
                        />
                        <Plus
                          @click="addOption(q.questionKey)"
                          class="hover:cursor-pointer"
                        /><Trash
                          @click="deleteOption(q.questionKey, option)"
                          class="hover:cursor-pointer"
                        />
                      </div>
                    </div>
                  </div>
                </div>
              </div>
              <div class="flex text-white gap-8 justify-end items-center mt-4">
                <div class="flex items-center">
                  <input
                    v-model="q.required"
                    type="checkbox"
                    :id="q.questionKey"
                    class="toggle"
                  />
                  <label
                    :for="q.questionKey"
                    class="text-black text-xl relative flex items-center curesor-pointer after:content-[''] after:w-[2em] after:h-[1em] after:bg-red-300 after:rounded-[1em] after:transition after:ml-[0.25em] after:duration-300 after:ease-in-out before:content-[''] before:flex before:justify-center before:items-center before:absolute before:w-[0.7em] before:right-[1.1em] before:h-[0.7em] before:bg-red-500 before:rounded-[1em] before:transition before:ml-[0.25em] before:duration-300 before:ease-in-out"
                    :class="{
                      'after:bg-green-200 before:content-[\'\'] before:translate-x-[0.9em] before:bg-green-500':
                        q.required,
                    }"
                    >Required</label
                  >
                </div>
                <div class="flex text-xl gap-2">
                  <p class="text-black">Type:</p>
                  <div class="text-black relative">
                    <p
                      class="text-black hover:cursor-pointer flex gap-2 items-center"
                      @click="showFieldType(q.questionKey)"
                    >
                      {{
                        q.field.type.toUpperCase().slice(0, 1) +
                        q.field.type.slice(1)
                      }}
                      <ArrowDown
                        class="hover:cursor-pointer transition"
                        :class="
                          questionState.get(q.questionKey).showTypeBtn
                            ? 'rotate-180'
                            : ''
                        "
                      />
                    </p>
                    <ul
                      v-if="questionState.get(q.questionKey).showTypeBtn"
                      class="absolute z-[2] bg-slate-200 p-2 rounded-lg"
                    >
                      <li
                        class="hover:bg-slate-500 hover:cursor-pointer p-2"
                        value
                        @click="setType(q.questionKey, $event)"
                      >
                        text
                      </li>
                      <li
                        class="hover:bg-slate-500 hover:cursor-pointer p-2"
                        value
                        @click="setType(q.questionKey, $event)"
                      >
                        file
                      </li>
                      <li
                        class="hover:bg-slate-500 hover:cursor-pointer p-2"
                        value
                        @click="setType(q.questionKey, $event)"
                      >
                        checkbox
                      </li>
                      <li
                        class="hover:bg-slate-500 hover:cursor-pointer p-2"
                        value
                        @click="setType(q.questionKey, $event)"
                      >
                        radio
                      </li>
                    </ul>
                  </div>
                </div>
                <button
                  class="bg-red-600 w-[200px] rounded-lg p-3"
                  @click="deleteQuestion(questions.indexOf(q))"
                >
                  Delete Question
                </button>
              </div>
            </div>
          </li>
        </VueDraggable>
      </ul>
      <div class="flex items-center justify-between">
        <div
          v-show="showHelper"
          ref="helper"
          @click="helperFunction"
          class="w-full absolute z-[1] top-0 left-0"
        ></div>
        <button
          @click="addQuestion"
          class="w-[250px] bg-green-600 p-2 border rounded-lg text-white"
        >
          ADD QUESTION</button
        ><button
          v-if="questions.length"
          @click="saveForm"
          class="w-[250px] bg-blue-600 p-2 border rounded-lg text-white"
        >
          Save
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
input {
  outline: none;
}
input[type="file"] {
  display: none;
}

input[type="checkbox"].toggle {
  opacity: 0;
  position: absolute;
}
</style>

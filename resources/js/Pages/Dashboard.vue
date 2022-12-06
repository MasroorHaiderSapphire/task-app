<script setup>
import AuthenticatedLayout from "@/Layouts/AuthenticatedLayout.vue";
import { Head, Link, usePage } from "@inertiajs/inertia-vue3";
import { useForm } from "@inertiajs/inertia-vue3";

const form = useForm({
  title: null,
  additional_info: null,
  priority: null,
});

const props = defineProps({
  message: String,
  tasks: Object,
});

const taskPriorityClasses = (level) =>
  level == 1
    ? "bg-red-100 text-red-800 text-sm font-medium mr-2 px-2.5 py-0.5 rounded dark:bg-red-200 dark:text-red-900"
    : "bg-yellow-100 text-yellow-800 text-sm font-medium mr-2 px-2.5 py-0.5 rounded dark:bg-yellow-200 dark:text-yellow-900";
const taskPriorityLevel = (level) => (level == 1 ? "Important" : "Unimportant");

const addTask = () => {
  form.post(route("task.store"));
};
</script>

<template>
  <Head title="Dashboard" />

  <AuthenticatedLayout>
    <template #header>
      <h2
        class="
          font-semibold
          text-xl text-gray-800
          dark:text-gray-200
          leading-tight
        "
      >
        Dashboard
      </h2>
    </template>

    <div class="py-12">
      <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
        <div
          class="
            bg-white
            dark:bg-gray-800
            overflow-hidden
            shadow-sm
            sm:rounded-lg
          "
        >
          <div class="p-6 text-gray-900 dark:text-gray-100">
            <div
              v-if="message"
              id="toast-success"
              class="
                m-auto
                z-50
                flex
                items-center
                p-4
                mb-4
                w-full
                max-w-xs
                text-gray-500
                bg-white
                rounded-lg
                shadow
                dark:text-gray-400 dark:bg-gray-800
              "
              role="alert"
            >
              <div
                class="
                  inline-flex
                  flex-shrink-0
                  justify-center
                  items-center
                  w-8
                  h-8
                  text-green-500
                  bg-green-100
                  rounded-lg
                  dark:bg-green-800 dark:text-green-200
                "
              >
                <svg
                  aria-hidden="true"
                  class="w-5 h-5"
                  fill="currentColor"
                  viewBox="0 0 20 20"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    fill-rule="evenodd"
                    d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"
                    clip-rule="evenodd"
                  ></path>
                </svg>
                <span class="sr-only">Check icon</span>
              </div>
              <div class="ml-3 text-sm font-normal">
                Task added successfully.
              </div>
              <button
                @click="message = !message"
                type="button"
                class="
                  ml-auto
                  -mx-1.5
                  -my-1.5
                  bg-white
                  text-gray-400
                  hover:text-gray-900
                  rounded-lg
                  focus:ring-2 focus:ring-gray-300
                  p-1.5
                  hover:bg-gray-100
                  inline-flex
                  h-8
                  w-8
                  dark:text-gray-500
                  dark:hover:text-white
                  dark:bg-gray-800
                  dark:hover:bg-gray-700
                "
                data-dismiss-target="#toast-success"
                aria-label="Close"
              >
                <span class="sr-only">Close</span>
                <svg
                  aria-hidden="true"
                  class="w-5 h-5"
                  fill="currentColor"
                  viewBox="0 0 20 20"
                  xmlns="http://www.w3.org/2000/svg"
                >
                  <path
                    fill-rule="evenodd"
                    d="M4.293 4.293a1 1 0 011.414 0L10 8.586l4.293-4.293a1 1 0 111.414 1.414L11.414 10l4.293 4.293a1 1 0 01-1.414 1.414L10 11.414l-4.293 4.293a1 1 0 01-1.414-1.414L8.586 10 4.293 5.707a1 1 0 010-1.414z"
                    clip-rule="evenodd"
                  ></path>
                </svg>
              </button>
            </div>
            <h2 class="text-xl text-gray-700 dark:text-white text-center">
              Add Task
            </h2>
            <hr class="my-2" />
            <form @submit.prevent="addTask">
              <div class="mb-6">
                <label
                  for="title"
                  class="
                    block
                    mb-2
                    text-sm
                    font-medium
                    text-gray-900
                    dark:text-white
                  "
                  >Benchmark Title</label
                >
                <input
                  v-model="form.title"
                  type="text"
                  id="title"
                  class="
                    shadow-sm
                    bg-gray-50
                    border border-gray-300
                    text-gray-900 text-sm
                    rounded-lg
                    focus:ring-blue-500 focus:border-blue-500
                    block
                    w-full
                    p-2.5
                    dark:bg-gray-700
                    dark:border-gray-600
                    dark:placeholder-gray-400
                    dark:text-white
                    dark:focus:ring-blue-500
                    dark:focus:border-blue-500
                    dark:shadow-sm-light
                  "
                  placeholder="Enter game title"
                  required
                />
              </div>
              <div class="mb-6">
                <label
                  for="additional_info"
                  class="
                    block
                    mb-2
                    text-sm
                    font-medium
                    text-gray-900
                    dark:text-white
                  "
                  >Additional info</label
                >
                <textarea
                  v-model="form.additional_info"
                  id="additional_info"
                  rows="4"
                  class="
                    block
                    p-2.5
                    w-full
                    text-sm text-gray-900
                    bg-gray-50
                    rounded-lg
                    border border-gray-300
                    focus:ring-blue-500 focus:border-blue-500
                    dark:bg-gray-700
                    dark:border-gray-600
                    dark:placeholder-gray-400
                    dark:text-white
                    dark:focus:ring-blue-500
                    dark:focus:border-blue-500
                  "
                  placeholder="Enter additional info"
                ></textarea>
              </div>
              <div class="mb-6">
                <label
                  for="countries"
                  class="
                    block
                    mb-2
                    text-sm
                    font-medium
                    text-gray-900
                    dark:text-white
                  "
                  >Priority</label
                >
                <select
                  v-model="form.priority"
                  id="countries"
                  class="
                    bg-gray-50
                    border border-gray-300
                    text-gray-900 text-sm
                    rounded-lg
                    focus:ring-blue-500 focus:border-blue-500
                    block
                    w-full
                    p-2.5
                    dark:bg-gray-700
                    dark:border-gray-600
                    dark:placeholder-gray-400
                    dark:text-white
                    dark:focus:ring-blue-500
                    dark:focus:border-blue-500
                  "
                  required
                >
                  <option value="1">Important</option>
                  <option value="2">Unimportant</option>
                </select>
              </div>
              <button
                type="submit"
                class="
                  block
                  w-full
                  text-white
                  bg-blue-700
                  hover:bg-blue-800
                  focus:ring-4 focus:outline-none focus:ring-blue-300
                  font-medium
                  rounded-lg
                  text-sm
                  px-5
                  py-2.5
                  text-center
                  dark:bg-blue-600
                  dark:hover:bg-blue-700
                  dark:focus:ring-blue-800
                "
                :disabled="form.processing"
                :class="{ 'opacity-25': form.processing }"
              >
                Add
              </button>
              <div class="text-center text-yellow-100 mt-2" v-if="form.isDirty">
                There are unsaved form changes.
              </div>
            </form>
            <div class="mt-5">
              <hr class="my-2" />
              <h2 class="text-xl text-gray-700 dark:text-white text-center">
                Tasks
              </h2>
              <hr class="my-2" />

              <div
                class="
                  grid grid-cols-1
                  md:grid-cols-2
                  lg:grid-cols-3
                  place-items-center
                  gap-4
                "
              >
                <div
                  v-for="task in tasks"
                  :key="task"
                  class="
                    w-full
                    p-6
                    bg-white
                    border border-gray-200
                    rounded-lg
                    shadow-md
                    dark:bg-gray-800 dark:border-gray-700
                  "
                >
                  <span
                    class="my-2 inline-block animate-pulse"
                    :class="taskPriorityClasses(task.priority)"
                    v-html="taskPriorityLevel(task.priority)"
                  ></span>

                  <h3>
                    <h5
                      class="
                        mb-2
                        text-2xl
                        font-semibold
                        tracking-tight
                        text-gray-900
                        dark:text-white
                      "
                    >
                      {{ task.title }}
                    </h5>
                  </h3>
                  <p
                    class="mb-3 font-normal text-gray-500 dark:text-gray-400"
                    v-if="task.additional_info"
                  >
                    {{ task.additional_info }}
                  </p>
                  <Link
                    :href="route('task.destroy', task.id)"
                    method="delete"
                    preserve-scroll
                    class="
                      inline-flex
                      items-center
                      px-3
                      py-2
                      text-sm
                      font-medium
                      text-center text-white
                      bg-green-700
                      rounded-lg
                      hover:bg-green-800
                      focus:ring-4 focus:outline-none focus:ring-green-300
                      dark:bg-green-600
                      dark:hover:bg-green-700
                      dark:focus:ring-green-800
                    "
                  >
                    <svg
                      xmlns="http://www.w3.org/2000/svg"
                      fill="none"
                      viewBox="0 0 24 24"
                      stroke-width="1.5"
                      stroke="currentColor"
                      class="w-5 h-5"
                    >
                      <path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        d="M9 12.75L11.25 15 15 9.75M21 12a9 9 0 11-18 0 9 9 0 0118 0z"
                      />
                    </svg>
                  </Link>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </AuthenticatedLayout>
</template>

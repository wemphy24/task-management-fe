<template>
  <div class="lg:pr-[70px] py-[50px] lg:ml-[320px] xl:ml-[365px] px-4 lg:pl-0">
    <!-- Top Section -->
    <section
      class="flex flex-col flex-wrap justify-between gap-6 md:items-center md:flex-row"
    >
      <div class="flex items-center justify-between gap-4">
        <a href="#" id="toggleOpenSidebar" class="lg:hidden">
          <svg
            class="w-6 h-6 text-dark"
            fill="none"
            stroke="currentColor"
            viewBox="0 0 24 24"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              stroke-linecap="round"
              stroke-linejoin="round"
              stroke-width="2"
              d="M4 6h16M4 12h16M4 18h7"
            ></path>
          </svg>
        </a>
        <div class="text-[32px] font-semibold text-dark">Tasks</div>
      </div>
      <div class="flex items-center gap-4">
        <form class="shrink md:w-[516px] w-full">
          <input
            type="text"
            name=""
            id=""
            class="input-field !outline-none !border-none italic form-icon-search ring-indigo-200 focus:ring-2 transition-all duration-300 w-full"
            placeholder="Search people, team, project"
          />
        </form>
        <a
          href="#"
          class="flex-none w-[46px] h-[46px] bg-white rounded-full p-[11px] relative notification-dot"
        >
          <img src="/assets/svgs/ic-bell.svg" alt="" />
        </a>
      </div>
    </section>

    <section class="pt-[50px]">
      <!-- Section Header -->
      <div class="mb-[30px]">
        <div
          class="flex flex-col justify-end gap-6 sm:items-center sm:flex-row"
        >
          <NuxtLink :to="{ name: 'tasks-create' }" class="btn btn-primary"
            >Add Task</NuxtLink
          >
        </div>
      </div>

      <div class="flex-auto block py-8 pt-6 px-9">
        <div class="overflow-x-auto">
          <table class="w-full my-0 align-middle text-dark border-neutral-200">
            <thead class="align-bottom">
              <tr class="font-semibold text-[0.95rem] text-secondary-dark">
                <th class="text-start">Title</th>
                <th class="text-end">Description</th>
                <th class="text-end">Due Date</th>
                <th class="text-end">Assign By</th>
                <th class="text-end">Assign To</th>
                <th class="text-end">Start</th>
                <th class="text-end">Complete</th>
                <th class="text-end">Status</th>
                <th class="text-end">Detail</th>
              </tr>
            </thead>
            <tbody>
              <p v-if="$fetchState.pending">Fetching tasks...</p>
              <p v-else>Task not found</p>
              <tr
                class="border-b border-dashed last:border-b-0"
                v-for="task in tasks.data.result.data"
                :key="task.id"
              >
                <td class="p-3 pl-0">
                  <div class="flex items-center">
                    <div class="flex flex-col justify-start">
                      <p
                        class="mb-1 font-semibold transition-colors duration-200 ease-in-out text-lg/normal text-secondary-inverse hover:text-primary"
                      >
                        {{ task.title }}
                      </p>
                    </div>
                  </div>
                </td>
                <td class="pr-0 text-end">
                  <span
                    class="font-semibold text-light-inverse text-md/normal"
                    >{{ task.description }}</span
                  >
                </td>
                <td class="pr-0 text-end">
                  <span
                    class="text-center align-baseline inline-flex px-2 py-1 mr-auto items-center font-semibold text-base/none text-success bg-success-light rounded-lg"
                  >
                    <svg
                      xmlns="http://www.w3.org/2000/svg"
                      fill="none"
                      viewBox="0 0 24 24"
                      stroke-width="1.5"
                      stroke="currentColor"
                      class="w-5 h-5 mr-1"
                    >
                      <path
                        stroke-linecap="round"
                        stroke-linejoin="round"
                        d="M2.25 18L9 11.25l4.306 4.307a11.95 11.95 0 015.814-5.519l2.74-1.22m0 0l-5.94-2.28m5.94 2.28l-2.28 5.941"
                      />
                    </svg>
                    {{ task.due_date }}
                  </span>
                </td>
                <td class="p-3 pr-12 text-end">
                  <span
                    class="text-center align-baseline inline-flex px-4 py-3 mr-auto items-center font-semibold text-[.95rem] leading-none text-primary bg-primary-light rounded-lg"
                  >
                    {{ task.assign_by }}
                  </span>
                </td>
                <td class="pr-0 text-start">
                  <span
                    class="font-semibold text-light-inverse text-md/normal"
                    >{{ task.id }}</span
                  >
                </td>

                <td class="p-3 pr-0 text-end">
                  <span
                    class="font-semibold text-light-inverse text-md/normal"
                    >{{ task.task_start }}</span
                  >
                </td>
                <td class="p-3 pr-0 text-end">
                  <span
                    class="font-semibold text-light-inverse text-md/normal"
                    >{{ task.task_complete }}</span
                  >
                </td>
                <td class="p-3 pr-0 text-end">
                  <span
                    class="font-semibold text-light-inverse text-md/normal"
                    >{{ task.status }}</span
                  >
                </td>
                <td class="p-3 pr-0 text-end">
                  <button
                    class="ml-auto relative text-secondary-dark bg-light-dark hover:text-primary flex items-center h-[25px] w-[25px] text-base font-medium leading-normal text-center align-middle cursor-pointer rounded-2xl transition-colors duration-200 ease-in-out shadow-none border-0 justify-center"
                  >
                    <span
                      class="flex items-center justify-center p-0 m-0 leading-none shrink-0"
                    >
                      <svg
                        xmlns="http://www.w3.org/2000/svg"
                        fill="none"
                        viewBox="0 0 24 24"
                        stroke-width="1.5"
                        stroke="currentColor"
                        class="w-4 h-4"
                      >
                        <path
                          stroke-linecap="round"
                          stroke-linejoin="round"
                          d="M8.25 4.5l7.5 7.5-7.5 7.5"
                        />
                      </svg>
                    </span>
                  </button>
                </td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
export default {
  layout: 'dashboard',
  middleware: 'auth',

  data() {
    return {
      tasks: [],
    }
  },

  async fetch() {
    this.tasks = await this.$axios.get('/task', {
      params: { limit: 8 },
    })
  },
  methods: {},
}
</script>

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

      <!-- Section Table -->
      <div class="flex flex-col">
        <table class="items-center bg-transparent border-collapse">
          <thead>
            <tr>
              <th
                class="px-2 bg-blueGray-50 align-middle border border-solid border-blueGray-100 py-3 text-sm uppercase border-l-0 border-r-0 font-semibold text-left"
              >
                Title
              </th>
              <th
                class="px-2 bg-blueGray-50 align-middle border border-solid border-blueGray-100 py-3 text-sm uppercase border-l-0 border-r-0 font-semibold text-left"
              >
                Description
              </th>
              <th
                class="px-2 bg-blueGray-50 align-middle border border-solid border-blueGray-100 py-3 text-sm uppercase border-l-0 border-r-0 font-semibold text-left"
              >
                Due Date
              </th>
              <th
                class="px-2 bg-blueGray-50 align-middle border border-solid border-blueGray-100 py-3 text-sm uppercase border-l-0 border-r-0 font-semibold text-left"
              >
                Assign By
              </th>
              <th
                class="px-2 bg-blueGray-50 align-middle border border-solid border-blueGray-100 py-3 text-sm uppercase border-l-0 border-r-0 font-semibold text-left"
              >
                Assign To
              </th>
              <th
                class="px-2 bg-blueGray-50 align-middle border border-solid border-blueGray-100 py-3 text-sm uppercase border-l-0 border-r-0 font-semibold text-left"
              >
                Status
              </th>
              <th
                class="px-2 bg-blueGray-50 align-middle border border-solid border-blueGray-100 py-3 text-sm uppercase border-l-0 border-r-0 font-semibold text-left"
              >
                Start
              </th>
              <th
                class="px-2 bg-blueGray-50 align-middle border border-solid border-blueGray-100 py-3 text-sm uppercase border-l-0 border-r-0 font-semibold text-left"
              >
                Complete
              </th>
              <th
                class="px-2 bg-blueGray-50 align-middle border border-solid border-blueGray-100 py-3 text-sm uppercase border-l-0 border-r-0 font-semibold text-left"
              >
                Action
              </th>
            </tr>
          </thead>

          <p v-if="$fetchState.pending">Fetching tasks...</p>
          <tbody v-else>
            <tr v-for="task in tasks.data.result.data" :key="task.id">
              <th
                class="border-t-0 align-middle border-l-0 border-r-0 text-base p-2 text-left"
              >
                {{ task.title }}
              </th>
              <td class="border-t-0 align-middle border-l-0 border-r-0 p-2">
                {{ task.description }}
              </td>
              <td class="border-t-0 align-center border-l-0 border-r-0 p-2">
                {{ task.due_date }}
              </td>
              <td class="border-t-0 align-center border-l-0 border-r-0 p-2">
                {{ task.assign_by }}
              </td>
              <td class="border-t-0 align-center border-l-0 border-r-0 p-2">
                {{ task.user['name'] }}
              </td>
              <td class="border-t-0 align-center border-l-0 border-r-0 p-2">
                {{ task.status }}
              </td>
              <td class="border-t-0 align-center border-l-0 border-r-0 p-2">
                {{ task.task_start }}
              </td>
              <td class="border-t-0 align-middle border-l-0 border-r-0 p-2">
                <i class="fas fa-arrow-up text-emerald-500 mr-4"></i>
                <div v-if="task.task_complete">
                  {{ task.task_complete }}
                </div>
                <div v-else>
                  <p>Not Finished</p>
                </div>
              </td>
              <td class="border-t-0 align-center border-l-0 border-r-0 p-2">
                <NuxtLink
                  :to="{ name: 'tasks-id', params: { id: task.id } }"
                  class="btn btn-primary"
                  >Detail</NuxtLink
                >
              </td>
            </tr>
          </tbody>
        </table>
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
    return
  },
  methods: {},
}
</script>

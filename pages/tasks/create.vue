<template>
  <section class="py-[70px] flex flex-col items-center justify-center px-4">
    <div class="text-[32px] font-semibold text-dark">New Task</div>
    <p class="my-4 text-base leading-7 text-center text-grey">
      Create task for user
    </p>
    <form class="w-full card" @submit.prevent="createTask">
      <div class="form-group">
        <label for="" class="text-grey">Title</label>
        <input type="text" class="input-field" v-model="task.title" />
      </div>
      <div class="form-group">
        <label for="" class="text-grey">Description</label>
        <input type="text" class="input-field" v-model="task.description" />
      </div>
      <div class="form-group">
        <label for="" class="text-grey">Due Date</label>
        <input
          type="datetime-local"
          class="input-field"
          v-model="task.due_date"
        />
      </div>
      <!-- <div class="form-group">
        <label for="" class="text-grey">Assign By</label>
        <input type="text" class="input-field" v-model="this.$auth.user.name" />
      </div> -->

      <div class="form-group">
        <label class="text-grey">Assign To</label>
        <p v-if="$fetchState.pending">Fetching users...</p>
        <select
          v-else
          v-model="task.user_id"
          name="users"
          id=""
          class="appearance-none input-field form-icon-chevron_down"
        >
          <option
            v-for="user in users.data.result"
            :value="user.id"
            :key="user.id"
          >
            {{ user.name }}
          </option>
        </select>
      </div>
      <!-- <div class="form-group">
        <label for="" class="text-grey">Status</label>
        <select
          v-model="task.selectedStatus"
          id=""
          class="appearance-none input-field form-icon-chevron_down"
        >
          <option value="Pending">Pending</option>
          <option value="In Progress">In Progress</option>
          <option value="Complete">Complete</option>
        </select>
      </div> -->
      <button type="submit" class="w-full btn btn-primary mt-[14px]">
        Create Task
      </button>
    </form>
  </section>
</template>

<script>
export default {
  layout: 'form',
  middleware: 'auth',

  data() {
    return {
      task: {
        title: '',
        description: '',
        due_date: '',
        assign_by: this.$auth.user.name,
        user_id: '',
        status: 'Pending',
        task_start: '',
        task_complete: '',
      },
      users: [],
      // selectedStatus: '',
    }
  },

  async fetch() {
    this.users = await this.$axios.get('/getalluser')
  },
  methods: {
    async createTask() {
      try {
        // send task data to server API
        const response = await this.$axios.post('/task', this.task)

        // redirect to task page
        this.$router.push({ name: 'tasks' })

        console.log(response)
      } catch (error) {
        console.log(error)
      }
    },
  },
}
</script>

<style></style>

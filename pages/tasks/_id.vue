<template>
  <section class="py-[70px] flex flex-col items-center justify-center px-4">
    <div class="text-[32px] font-semibold text-dark">Edit Task</div>
    <p class="my-4 text-base leading-7 text-center text-grey">
      Edit task for user
    </p>

    <form class="w-full card" @submit.prevent="editTask">
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
          step="any"
          type="datetime-local"
          class="input-field"
          v-model="task.due_date"
        />
      </div>

      <button type="submit" class="w-full btn btn-primary mt-[14px]">
        Edit Task
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
      task: [],
      taskId: '',
    }
  },

  mounted() {
    this.taskId = this.$route.params.id
    this.getTask(this.taskId)
  },
  methods: {
    async getTask(taskId) {
      this.$axios.get(`/task/edit/${taskId}`).then((res) => {
        this.task = res.data.result
        // console.log(res)
      })
    },

    async editTask() {
      this.$axios.put(`/task/update/${this.taskId}`, this.task).then((res) => {
        this.$router.push({ name: 'tasks' })
        // console.log(res)
      })
    },
  },
}
</script>

<style></style>

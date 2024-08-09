<template>
  <section class="py-[70px] flex flex-col items-center justify-center px-4">
    <div class="text-[32px] font-semibold text-dark">New Role</div>
    <p class="my-4 text-base leading-7 text-center text-grey">
      Create role for user
    </p>
    <form class="w-full card" @submit.prevent="createRole">
      <div class="form-group">
        <label for="" class="text-grey">Role Name</label>
        <input type="text" class="input-field" v-model="role.name" />
      </div>
      <button type="submit" class="w-full btn btn-primary mt-[14px]">
        Save Role
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
      role: {
        name: '',
      },
    }
  },
  methods: {
    async createRole() {
      try {
        // send team data to server API
        const response = await this.$axios.post('/role', this.role)

        // redirect to role page
        this.$router.push({ name: 'roles' })

        console.log(response)
      } catch (error) {
        console.log(error)
      }
    },
  },
}
</script>

<style></style>

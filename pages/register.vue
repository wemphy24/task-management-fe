<template>
  <div>
    <section class="py-[50px] flex flex-col items-center justify-center px-4">
      <img src="/assets/svgs/logo-type.svg" alt="" />
      <div class="text-[32px] font-semibold text-dark mt-[70px]">Sign Up</div>
      <p class="mt-4 text-base leading-7 text-center mb-[50px] text-grey">
        Manage your employees to achieve <br />
        a bigger goals for your company
      </p>
      <form class="w-full card" @submit.prevent="userRegister">
        <div class="form-group">
          <label for="" class="text-grey">Name</label>
          <input type="text" class="input-field" v-model="register.name" />
        </div>
        <div class="form-group">
          <label for="" class="text-grey">Email Address</label>
          <input type="email" class="input-field" v-model="register.email" />
        </div>
        <div class="form-group">
          <label for="" class="text-grey">Password</label>
          <input
            type="password"
            class="input-field"
            v-model="register.password"
          />
        </div>
        <button type="submit" class="w-full btn btn-primary mt-[14px]">
          Continue
        </button>
      </form>
    </section>
  </div>
</template>

<script>
export default {
  auth: 'guest',
  data() {
    return {
      register: {
        name: '',
        email: '',
        password: '',
        role_id: 2,
      },
    }
  },
  methods: {
    async userRegister() {
      try {
        // send register data to server API
        const response = await this.$axios.post('/register', this.register)
        // if success login
        try {
          const login = await this.$auth.loginWith('local', {
            data: {
              email: this.register.email,
              password: this.register.password,
            },
          })
          console.log(login)
        } catch (err) {
          console.log(err)
        }
        console.log(response)
        // ----------
      } catch (error) {
        console.log(error)
      }
    },
  },
}
</script>

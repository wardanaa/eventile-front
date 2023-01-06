<template>
  <div class="min-h-screen bg-gray-200">
    <div class="flex justify-center">
      <div class="rounded border shadow-sm p-4 my-12 w-4/12 bg-white">
        <h1 class="text-center text-2xl">Create Account</h1>
        <form
          class="flex flex-wrap justify-center my-10"
          @submit.prevent="submit"
        >
          <div class="w-full flex flex-wrap justify-center mt-10">
            <input
              v-model="form.name"
              type="text"
              class="p-2 rounded border shadow-sm w-9/12"
              placeholder="Your Awesome Name"
            />
            <error-field :errors="errors" field="name" />
          </div>
          <div class="w-full flex flex-wrap justify-center mt-10">
            <input
              v-model="form.email"
              type="email"
              class="p-2 rounded border shadow-sm w-9/12"
              placeholder="Your Awesome Email"
            />
            <error-field :errors="errors" field="email" />
          </div>
          <div class="w-full flex flex-wrap justify-center mt-10">
            <input
              v-model="form.password"
              type="password"
              class="p-2 rounded border shadow-sm w-9/12"
              placeholder="Super Secret Password"
            />
            <error-field :errors="errors" field="password" />
          </div>
          <div class="w-full flex flex-wrap justify-center mt-10">
            <input
              v-model="form.password_confirmation"
              type="text"
              class="p-2 rounded border shadow-sm w-9/12"
              placeholder="Re write same password"
            />
            <error-field :errors="errors" field="password_confirmation" />
          </div>

          <div class="w-full flex justify-center mt-10">
            <input
              type="submit"
              class="p-2 rounded border shadow-sm w-9/12 bg-blue-600 text-white font-semibold cursor-pointer"
              value="Register"
            />
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import ErrorField from '../components/util/ErrorField'
export default {
  components: { ErrorField },
  data() {
    return {
      form: {
        email: 'sarthak@bitfumes.com',
        name: 'Sarthak',
        password: 'password',
        password_confirmation: 'password'
      },
      errors: {}
    }
  },
  methods: {
    submit() {
      this.$axios
        .$post('register', this.form)
        .then((res) => {
          this.$router.push('/login')
        })
        .catch((e) => (this.errors = e.response.data.errors))
    }
  }
}
</script>

<style></style>

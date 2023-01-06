<template>
  <div class="min-h-screen bg-gray-200">
    <div class="flex justify-center">
      <div class="rounded border shadow-sm p-4 my-12 w-10/12 bg-white">
        <h1 class="text-center text-2xl">Create New Event</h1>
        <form
          class="flex flex-wrap justify-center my-10"
          @submit.prevent="submit"
        >
          <div class="w-full flex flex-wrap justify-center mt-10">
            <input
              type="file"
              class="p-2 rounded border shadow-sm w-9/12"
              @change="handleFile"
            />
            <error-field :errors="errors" field="image" />
          </div>
          <div class="w-full flex flex-wrap justify-center mt-10">
            <input
              v-model="form.name"
              type="text"
              class="p-2 rounded border shadow-sm w-9/12"
              placeholder="Event Name"
            />
            <error-field :errors="errors" field="name" />
          </div>

          <div class="w-full flex flex-wrap justify-center mt-10">
            <div class="w-9/12 flex justify-between">
              <div class="w-5/12">
                <textarea
                  class="p-2 rounded border shadow-sm w-full"
                  v-model="form.description"
                  cols="30"
                  rows="3"
                  placeholder="What is this event for ?"
                ></textarea>
                <error-field :errors="errors" field="description" />
              </div>
              <div class="w-5/12">
                <textarea
                  class="p-2 rounded border shadow-sm w-full"
                  v-model="form.address"
                  cols="30"
                  rows="3"
                  placeholder="Event Address"
                ></textarea>
                <error-field :errors="errors" field="address" />
              </div>
            </div>
          </div>

          <div class="w-full flex flex-wrap justify-center mt-10">
            <div class="w-9/12 flex justify-between">
              <div class="w-5/12">
                <input
                  v-model="form.ticket_price"
                  type="number"
                  class="p-2 rounded border shadow-sm w-full"
                  placeholder="Event Price"
                />
                <error-field :errors="errors" field="ticket_price" />
              </div>
              <div class="w-5/12">
                <input
                  v-model="form.ticket_remaining"
                  type="number"
                  class="p-2 rounded border shadow-sm w-full"
                  placeholder="Event Total Number of Tickets"
                />
                <error-field :errors="errors" field="ticket_remaining" />
              </div>
            </div>
          </div>

          <div class="w-full flex flex-wrap justify-center mt-10">
            <div class="w-9/12 flex justify-between">
              <div class="w-5/12">
                <label for="date" class="text-gray-600"
                  >Publish This Event At</label
                >
                <input
                  v-model="form.published_at"
                  type="date"
                  class="p-2 rounded border shadow-sm w-full"
                  placeholder="Publish Date of Event"
                />
                <error-field :errors="errors" field="published_at" />
              </div>
              <div class="w-5/12">
                <label for="date" class="text-gray-600">Date Of Event</label>
                <input
                  v-model="form.date"
                  type="date"
                  class="p-2 rounded border shadow-sm w-full"
                  placeholder="Date Of Event"
                />
                <error-field :errors="errors" field="date" />
              </div>
            </div>
          </div>

          <div class="w-full flex justify-center mt-10">
            <input
              type="submit"
              class="p-2 rounded border shadow-sm w-9/12 bg-blue-600 text-white font-semibold cursor-pointer"
              value="Create"
            />
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import ErrorField from '../../components/util/ErrorField'
export default {
  middleware: 'admin',
  components: { ErrorField },
  data() {
    return {
      form: {
        name: '',
        description: '',
        address: '',
        image: '',
        ticket_price: '',
        ticket_remaining: '',
        published_at: '',
        date: ''
      },
      errors: {}
    }
  },
  methods: {
    handleFile(e) {
      this.form.image = e.target.files[0]
    },
    submit() {
      const NewForm = new FormData()
      Object.keys(this.form).forEach((key) => {
        NewForm.set(key, this.form[key])
      })
      this.$axios
        .$post('event', NewForm, {
          headers: {
            'content-type': 'multiform/form-data'
          }
        })
        .then((res) => {
          this.$router.push('/event')
        })
        .catch((e) => (this.errors = e.response.data.errors))
    }
  }
}
</script>

<style></style>

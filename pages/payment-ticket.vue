<template>
  <div class="flex justify-center">
    <div class="w-10/12">
      <section class="bg-gray-100 my-4 p-4 rounded shadow">
        <h1 class="text-2xl my-2">Tickets Purchase History</h1>
        <div v-for="(ticket, i) in tickets" :key="i">
          <div
            class="flex justify-between bg-gray-300 rounded shadow p-2 my-2 text-gray-800"
          >
            <p>{{ ticket.event.name }}</p>
            <p>Tickets Count {{ ticket.ticket_count }}</p>
            <p>{{ ticket.created_at }}</p>
          </div>
        </div>
      </section>
      <section class="bg-gray-100 my-4 p-4 rounded shadow">
        <h1 class="text-2xl my-2">Payments History</h1>
        <div v-for="(payment, i) in payments" :key="i">
          <div
            class="flex justify-between bg-gray-300 rounded shadow p-2 my-2 text-gray-800"
          >
            <p class="text-sm">{{ payment.product.name }}</p>
            <p class="text-sm">{{ payment.payment_id }}</p>
            <p class="text-sm">{{ payment.amount }}</p>
            <p class="text-sm">{{ payment.created_at }}</p>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
export default {
  async asyncData({ query, $axios, redirect, app }) {
    const data = await $axios.$get(`/payment`)
    const tickets = await $axios.$get(`/ticket`)
    return { payments: data.data, tickets: tickets.data }
  }
}
</script>

<style></style>

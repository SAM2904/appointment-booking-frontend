<template>
  <div style="margin-top: 20px;">
    <h3>Book Appointment</h3>

    <p>
      Selected:
      <strong>Start {{ slot.start }} - End {{ slot.end }}</strong>
    </p>

    <input
      type="email"
      placeholder="Enter your email"
      v-model="email"
    />

    <br /><br />

    <button @click="book">Book</button>

    <p v-if="message">{{ message }}</p>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  props: {
    slot: Object,
    serviceId: Number,
    selectedDate: String
  },
  data() {
    return {
      email: '',
      message: ''
    }
  },
  methods: {
    async book() {
      try {
        await axios.post('http://localhost:8000/api/bookings', {
          service_id: this.serviceId,
          start_at: this.slot.start,
          client_email: this.email
        })

        this.message = 'Booking successful'

        setTimeout(() => {
          window.location.reload()
        }, 1000)
      } catch (error) {
        if (error.response) {
          if (error.response.status == 422) {
            this.message = error.response.data.message ?? 'Slot already booked or invalid.'
          }else{
            this.message = 'Something went wrong!'
          }
        }
      }
    }
  }
}
</script>

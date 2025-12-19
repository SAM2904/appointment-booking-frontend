<template>
  <div style="padding:20px;font-family:Arial">

    <h2>Smart Booking Scheduler</h2>

    <!-- Toggle -->
    <button @click="mode = 'client'">Client Booking</button>
    <button @click="mode = 'admin'" style="margin-left:10px">
      Admin Working Hours
    </button>

    <hr />

    <!-- CLIENT MODE -->
    <div v-if="mode === 'client'">
      <h3>Client - Appointment Booking</h3>

      <DatePicker @date-selected="onDateChange" />

      <TimeSlots
        :slots="slots"
        @select="onSlotSelect"
      />

      <BookingForm
        v-if="selectedSlot"
        :slot="selectedSlot"
        :serviceId="serviceId"
      />
    </div>

    <!-- ADMIN MODE -->
    <div v-else>
      <AdminWorkingHours />
    </div>

  </div>
</template>

<script>
import axios from 'axios'
import DatePicker from './components/DatePicker.vue'
import TimeSlots from './components/TimeSlots.vue'
import BookingForm from './components/BookingForm.vue'
import AdminWorkingHours from './components/AdminWorkingHours.vue'

export default {
  components: {
    DatePicker,
    TimeSlots,
    BookingForm,
    AdminWorkingHours
  },
  data() {
    return {
      mode: 'client',
      selectedDate: '',
      slots: [],
      selectedSlot: null,
      serviceId: 1
    }
  },
  methods: {
    async onDateChange(date) {
      this.selectedDate = date
      this.selectedSlot = null

      const res = await axios.get(
        'http://localhost:8000/api/availability',
        {
          params: {
            date,
            service_id: this.serviceId
          }
        }
      )

      this.slots = res.data.data || []
    },
    onSlotSelect(slot) {
      this.selectedSlot = slot
    }
  }
}
</script>

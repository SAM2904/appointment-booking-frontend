<template>
  <div>
    <h3>Admin - Manage Working Hours</h3>

    <!-- Add Rule -->
    <div style="margin-bottom:15px;">
      <select v-model="form.weekday_id">
        <option value="">Select Day</option>
        <option v-for="day in weekdays" :key="day.id" :value="day.id">
          {{ day.name }}
        </option>
      </select>

      <input type="time" v-model="form.start_time" />
      <input type="time" v-model="form.end_time" />

      <button @click="addRule">Add</button>
    </div>

    <!-- List Rules -->
    <table border="1" cellpadding="6">
      <thead>
        <tr>
          <th>Day</th>
          <th>Start</th>
          <th>End</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="rule in rules" :key="rule.id">
          <td>{{ rule.weekday_name }}</td>
          <td>{{ rule.start_time }}</td>
          <td>{{ rule.end_time }}</td>
        </tr>
      </tbody>
    </table>

    <p v-if="message">{{ message }}</p>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      weekdays: [],
      rules: [],
      message: '',
      form: {
        weekday_id: '',
        start_time: '',
        end_time: ''
      }
    }
  },
  mounted() {
    this.loadWeekdays()
    this.loadRules()
  },
  methods: {
    async loadWeekdays() {
      const res = await axios.get('http://localhost:8000/api/weekdays')
      this.weekdays = res.data.data || []
    },
    async loadRules() {
      const res = await axios.get(
        'http://localhost:8000/api/admin/working-hours/list'
      )
      this.rules = res.data.data || []
    },
    async addRule() {
      try {
        await axios.post(
          'http://localhost:8000/api/admin/working-hours/store',
          this.form
        )

        this.message = 'Working hour added successfully'
        this.form = { weekday_id: '', start_time: '', end_time: '' }
        this.loadRules()
      } catch (e) {
        this.message = e.response?.data?.message || 'Error'
      }
    }
  }
}
</script>

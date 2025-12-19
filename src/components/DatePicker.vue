<template>
  <div style="margin-bottom: 16px;">
    <label>
      Select Date:
      <input
        type="date"
        :min="today"
        v-model="selectedDate"
        @change="emitDate"
      />
    </label>
  </div>
</template>

<script>
export default {
  data() {
    return {
      selectedDate: '',
      today: new Date().toISOString().split('T')[0]
    }
  },
  methods: {
    emitDate() {
      this.$emit('date-selected', this.selectedDate)
    }
  }
}
</script>

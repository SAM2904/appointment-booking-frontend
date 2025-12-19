<template>
  <div>
    <h3>Available Time Slots</h3>

    <div v-if="slots.length === 0">
      No slots available
    </div>

    <div v-else>
      <button
        v-for="slot in slots"
        :key="slot.start"
        @click="select(slot)"
        style="margin: 4px;"
      >
        {{ slot.start.split(' ')[1] }} - {{ slot.end.split(' ')[1] }}
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    slots: {
      type: Array,
      required: true
    }
  },
  methods: {
    select(slot) {
      this.$emit('select', slot)
    }
  }
}
</script>

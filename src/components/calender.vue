<template>
  <div>
    <b-table
      hover
      responsive
      head-variant="dark"
      bordered
      :items="items" 
      :fields="fields">
    </b-table>
  </div>
</template>

<script>
// import dates from '../data/dates.json'
export default {
  props: {
    data: {
      type: Array,
      default: () => [],
    },
    tuples: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      items: [],
      fields: this.tuples
    }
  },
  mounted() {
    this.items = this.data
  },
  watch: {
    data(val) {
      this.items = val
    }
  }
}
</script>
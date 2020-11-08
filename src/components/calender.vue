<template>
  <div>
    <b-table striped hover :items="items" :fields="fields"></b-table>
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
    console.log(this.data)
  },
  watch: {
    data(val) {
      console.log(val)
      this.items = val
    }
  }
}
</script>
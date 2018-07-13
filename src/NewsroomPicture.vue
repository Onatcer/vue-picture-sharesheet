<template>
  <picture>
    <img :src=src>
  </picture>
</template>

<script>
  export default {
    model: {
      prop: 'model',
      event: 'change'
    },
    props: {
      src: String,
      alt: String
    },
    data: function () {
      return {
        srx: this.src
      }
    },
    computed: {
      classObject() {
      }
    },
    methods: {
      getDateType() {
      }
    },
    watch: {
      value(v) {
      }
    }
  }
</script>

<style lang="scss">

</style>

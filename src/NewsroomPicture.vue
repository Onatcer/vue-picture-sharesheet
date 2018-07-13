<template>
  <div class="image-container">
      <picture>
        <img :src=src :alt=alt :height=height :width=width>
      </picture>
  </div>

</template>

<script>
  export default {
    model: {
      prop: 'model',
      event: 'change'
    },
    props: {
      src: String,
      alt: String,
      height: String,
      width: String,
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

  picture {
    display: inline-block;

    /* HOVER OUT */
    transition: box-shadow .4s ease;
  }

  picture:hover {
    box-shadow: 0 39.275px 70px -14.275px rgba(0, 0, 0, 0.3);

    /* HOVER IN */
    transition: box-shadow .15s ease;
  }


</style>

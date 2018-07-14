<template>
  <div class="image-container">
    <div class="sharesheet-container" @mouseover="hovered = true" @mouseleave="hovered = false">

      <picture>
        <img :src=src :alt=alt :height=height :width=width>
      </picture>
      <transition name="fade">
        <Sharesheet v-if="hovered" class="sharesheet" @downloadImage="download"></Sharesheet>
      </transition>
    </div>
  </div>

</template>

<script>
  import Sharesheet from './Sharesheet.vue';

  export default {
    components: {
      Sharesheet
    },
    model: {
      prop: 'model',
      event: 'change'
    },
    data() {
      return {
        hovered: false
      }
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
      download() {
        let link = document.createElement('a');
        link.setAttribute('href', this.src);
        link.setAttribute('download', 'Filename.jpg');
        link.setAttribute('target', '_blank');
        link.style.display = 'none';
        document.body.appendChild(link);
        link.click();
        document.body.removeChild(link);
      }
    },
    watch: {
      value(v) {
      }
    }
  }
</script>

<style lang="scss">

  .image-container {
    display: block;
  }

  .sharesheet-container {
    display: inline-block;
    position: relative;

    /* HOVER OUT */
    transition: box-shadow .4s ease;
  }

  .sharesheet-container:hover {
    box-shadow: 0 39.275px 70px -14.275px rgba(0, 0, 0, 0.3);
    /* HOVER IN */
    transition: box-shadow .15s ease;
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity .3s;
  }
  .fade-enter, .fade-leave-to{
    opacity: 0;
  }

</style>

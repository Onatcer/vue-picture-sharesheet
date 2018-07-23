<template>
  <div class="image-container">
    <div class="sharesheet-container" @mouseover="hovered = true" @mouseleave="hovered = false" :class="{ shadow: showSharesheet }">

      <picture>
        <img
          :src=src
          :alt=alt
          :height=height
          :width=width
          :ismap=ismap
          :longdesc=longdesc
          :usemap=usemap
          :crossorigin=crossorigin>
      </picture>
      <transition name="fade">
        <Sharesheet
          v-if="showSharesheet"
          class="sharesheet"
          :sheetcolor=sheetcolor
          :iconcolor=iconcolor
          :position=position
          :size=size
          :sharemessage=sharemessage
          @downloadImage="download"
        />
      </transition>
    </div>
  </div>

</template>

<script>
  import Sharesheet from './Sharesheet.vue';

  export default {
    name: "picture-sharesheet",
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
      ismap: Boolean,
      longdesc: String,
      usemap: String,
      crossorigin: String,
      sheetcolor: String,
      iconcolor: String,
      position: String,
      size: String,
      sharemessage: String,
      fixed: Boolean
    },
    computed: {
      showSharesheet: function () {
        return (this.fixed) ? true : this.hovered;
      }
    },
    methods: {
      toDataURL(src, callback, outputFormat) {
        var img = new Image();
        img.crossOrigin = 'Anonymous';
        img.onload = function () {
          var canvas = document.createElement('CANVAS');
          var ctx = canvas.getContext('2d');
          var dataURL;
          canvas.height = this.naturalHeight;
          canvas.width = this.naturalWidth;
          ctx.drawImage(this, 0, 0);
          dataURL = canvas.toDataURL(outputFormat);
          callback(dataURL);
        };
        img.src = src;
        if (img.complete || img.complete === undefined) {
          img.src = "data:image/gif;base64,R0lGODlhAQABAIAAAAAAAP///ywAAAAAAQABAAACAUwAOw==";
          img.src = src;
        }
      },
      download() {
        let link = document.createElement('a');
        let filename = this.alt || 'download';
        this.toDataURL(
          this.src,
          function(dataUrl) {
            link.setAttribute('href', dataUrl);
            link.setAttribute('download', `${filename}.jpg`);
            link.setAttribute('target', '_blank');
            link.style.display = 'none';
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
          }, 'image/jpeg'
        );
      }
    },
    watch: {
      value(v) {
      }
    }
  }
</script>

<style lang="scss" scoped>

  .image-container {
    display: block;
    max-width: 100%;
  }

  .sharesheet-container {
    display: inline-block;
    position: relative;
    /* HOVER OUT */
    transition: box-shadow .4s ease;
    max-width: 100%;
  }
  picture, img{
    max-width: 100%;
  }

  .sharesheet-container:hover {
    box-shadow: 0 39.275px 70px -14.275px rgba(0, 0, 0, 0.3);
    /* HOVER IN */
    transition: box-shadow .15s ease;
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity .3s;
  }

  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

  .shadow{
    box-shadow: 0 39.275px 70px -14.275px rgba(0, 0, 0, 0.3)
  }
</style>

<template lang="html">

  <section class="sharesheet" v-bind:class="{ alert: showAlert }" :style="[{ 'background-color': sheetcolor }, SharesheetAttriputes]">
    <icon v-for="icon in icons" class="icon" :name="icon.icon" :style="[{ 'color': iconcolor }, IconsAttributes]"
          @click.native="clickHandler(icon.name)" :flip="icon.flip"
          :scale="icon.scale"></icon>
  </section>

</template>

<script lang="js">
  import Vue from 'vue'
  import 'vue-awesome/icons/facebook-square'
  import 'vue-awesome/icons/twitter'
  import 'vue-awesome/icons/link'
  import 'vue-awesome/icons/download'
  
  import Icon from 'vue-awesome/components/Icon'

  import VueClipboard from 'vue-clipboard2'

  Vue.use(VueClipboard);

  export default {
    name: 'sharesheet',
    props: {
      sheetcolor: String,
      iconcolor: String,
      sharemessage: String,
      size: {
        default: "55px",
        type: String
      },
      position: {
        default: "bottom",
        type: String
      },
    },

    components: {
      Icon
    },
    mounted() {

    },
    data() {
      return {
        showAlert: false,
        icons: [
          {
            name: "facebook",
            icon: "facebook-square",
            scale: 1.3,
          },
          {
            name: "twitter",
            icon: "twitter",
            scale: 1.3,
          },
          {
            name: "copy",
            icon: "link",
            scale: 1.2,
            flip: "horizontal"
          },
          {
            name: "download",
            icon: "arrow-circle-down",
            scale: 1.3
          }
        ]
      }
    },
    methods: {
      clickHandler: function (name) {
        switch (name) {
          case "facebook":
            this.openFacebookWindow();
            break;
          case "twitter":
            this.openTwitterWindow();
            break;
          case "copy":
            this.copyClipboard();
            break;
          case "download":
            this.$emit('downloadImage');
            break;
        }
      },
      openFacebookWindow: function (event) {
        let url = "https://www.facebook.com/sharer/sharer.php?u=" + decodeURI(window.location.href) +
          ((this.sharemessage.length !== 0) ? "&quote=" + this.sharemessage : "");
        window.open(url, '_blank', "toolbar=yes,scrollbars=yes,resizable=yes,top=200,left=200,width=600,height=400");
      },
      openTwitterWindow: function (event) {
        let url = "https://twitter.com/home?status=" +
          ((this.sharemessage.length !== 0) ? this.sharemessage : document.title) +
          " - " +
          window.location.href;
        window.open(url, '_blank', "toolbar=yes,scrollbars=yes,resizable=yes,top=200,left=200,width=600,height=400");
      },
      copyClipboard: function (event) {
        let that = this;
        this.$copyText(window.location.href).then(function (e) {
          that.showAlert = true;
          setTimeout(function () {
            that.showAlert = false;
          }, 2000);

        }, function (e) {
          alert('Can not copy');
          console.log(e)
        })
      }
    },
    computed: {
      SharesheetAttriputes() {
        let width, height, flexDirection, justifyContent, padding;

        if (this.position === 'left' || this.position === 'right') {
          height = "100%";
          width = this.size;
          flexDirection = "column";
          justifyContent = "center";
          padding= "30px 0";
        }

        if (this.position === 'bottom' || this.position === 'top') {
          height = this.size;
          width = "100%";
          flexDirection = "row";
          justifyContent = "left";
          padding= "0 30px";
        }

        return {
          'width': width,
          'height': height,
          'flex-direction': flexDirection,
          'justify-content': justifyContent,
          'padding': padding,
          [this.position]: "0px"
        }
      },
      IconsAttributes() {
        let marginRight, marginBottom;

        if (this.position === 'left' || this.position === 'right') {
          marginRight = "0px";
          marginBottom = "17px";

        }

        if (this.position === 'bottom' || this.position === 'top') {
          marginRight = "17px";
          marginBottom = "0px";
        }
        return {
          'margin-right': marginRight,
          'margin-bottom': marginBottom,
        }
      }
    },
  }
</script>

<style scoped lang="scss">
  @keyframes fadein {
    0% {
      opacity: 0;
      position: relative;
      left: -5px;
    }
    100% {
      opacity: 1;
      position: relative;
      left: 0px;
    }
  }

  .icon {
    color: #FFF;
    margin-right: 17px;
    opacity: 0.95;
    animation-name: fadein;
    animation-duration: 300ms;
    animation-fill-mode: both;
  }

  .icon:hover {
    color: #0070c9;
    cursor: pointer;
  }

  .sharesheet {
    position: absolute;
    text-align: left;
    background-color: rgba(34, 34, 34, 0.95);
    display: flex;
    align-items: center;
    justify-content: center;
    box-sizing: border-box;
    bottom: 0px;
  }

  .alert::before {
    content: 'Copied to Clipboard';
    font-family: Avenir, Helvetica, Arial, sans-serif;
    padding: 10px 15px;
    font-size: 0.9em;
    background-color: rgba(34, 34, 34, 0.95);
    color: #FFF;
    position: absolute;
    left: 10px;
    bottom: 70px;
  }

  @for $i from 1 through 10 {
    .icon:nth-of-type(#{$i}) {
      animation-delay: #{$i*100}ms;
    }
  }



</style>

<template lang="html">

  <section class="sharesheet" v-bind:class="{ alert: showAlert }">
    <icon v-for="icon in icons" class="icon" :name="icon.icon" @click.native="clickHandler(icon.name)"
          :scale="icon.scale"></icon>
  </section>

</template>

<script lang="js">
  import Vue from 'vue'
  import 'vue-awesome/icons';
  import Icon from 'vue-awesome/components/Icon'
  import VueClipboard from 'vue-clipboard2'

  Vue.use(VueClipboard);

  export default {
    name: 'sharesheet',
    props: [],
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
        }
      },
      openFacebookWindow: function (event) {
        window.open("https://www.facebook.com/sharer/sharer.php?u=" + decodeURI(window.location.href), '_blank', "toolbar=yes,scrollbars=yes,resizable=yes,top=200,left=200,width=600,height=400");
      },
      openTwitterWindow: function (event) {
        window.open("https://twitter.com/home?status=" + window.location.href, '_blank', "toolbar=yes,scrollbars=yes,resizable=yes,top=200,left=200,width=600,height=400");
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
    computed: {}
  }
</script>

<style scoped lang="scss">
  .icon {
    color: #FFF;
    margin-right: 17px;
    opacity: 0.95;
  }

  .icon:hover {
    color: #0070c9;
    cursor: pointer;
  }

  .sharesheet {
    position: absolute;
    bottom: 0px;
    left: 0;
    width: 100%;
    height: 55px;
    text-align: left;
    background-color: rgba(34, 34, 34, 0.95);
    padding: 0 30px;
    display: flex;
    align-items: center;
    box-sizing: border-box;
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
    top: -50px;
  }
</style>

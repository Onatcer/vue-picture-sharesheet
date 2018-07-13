<template lang="html">

  <section class="sharesheet">
    <icon class="icon" name="facebook-square" @click.native="openFacebookWindow" scale="1.3"></icon>
    <icon class="icon" name="twitter" scale="1.3" @click.native="openTwitterWindow"></icon>
    <icon class="icon" name="link" scale="1.2" flip="horizontal" @click.native="copyClipboard"></icon>
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
      return {}
    },
    methods: {
      openFacebookWindow: function (event) {
        window.open("https://www.facebook.com/sharer/sharer.php?u=" + decodeURI(window.location.href), '_blank', "toolbar=yes,scrollbars=yes,resizable=yes,top=200,left=200,width=600,height=400");
      },
      openTwitterWindow: function (event) {
        window.open("https://twitter.com/home?status=" + window.location.href, '_blank', "toolbar=yes,scrollbars=yes,resizable=yes,top=200,left=200,width=600,height=400");
      },
      copyClipboard: function (event){
        this.$copyText(window.location.href).then(function (e) {
          alert('Copied');
          console.log(e)
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
</style>

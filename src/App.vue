<template>
  <!-- Start products  -->
  <div class="Products">
    <div class="container">
      <div class="row">

        <!-- Call Popup components -->
        <Popup :product="product" v-if="showPopup" :class="{ showPopup : showPopup }" v-on:closePopup="closePopupMethod" />
     
        <!-- Call Product components -->
        <Product :product="product" v-for="product in products" :key="product.id" v-on:openPopup="openPopupMethod" />
      </div>
    </div>
  </div>
  <!-- End Products -->
</template>

<script>
  import Product from './components/Product.vue'
  import Popup from './components/Popup.vue'
  import axios from 'axios';
  import $ from 'jquery';

  export default {
    name: 'App',
    data() {
      return {
        product: {},
        products: [],
        errors: [],
        showPopup: false
      }
    },
    components: {
      Product,
      Popup
    },
    created() {
      // XHR call
      axios.get(`https://gs-euw1-public-data-prod.s3-eu-west-1.amazonaws.com/new-web/test/test.json`, {}, {
          headers: {
            'Content-type': 'application/x-www-form-urlencoded',
          }
        })
        .then(response => {
          var data = response.data
          this.products = data.hits
        })
        .catch(e => {
          this.errors.push(e)
        })
    },
    methods: {
      //  Open Modal
      openPopupMethod(product) {
        this.product = product
        this.showPopup = true
        $('body').addClass('modal-open')

      },

      //  Close Modal
      closePopupMethod() {
        this.product = {}
        this.showPopup = false
        $('body').removeClass('modal-open')

      }
    },
  }
</script>

<style lang="scss">
  @import 'components/sass/style.scss';
  //  If you need style file go to components/sass/style.scss
</style>

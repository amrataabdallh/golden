<template>
  <!-- Start products  -->
  <div class="Products">
    <div class="container">
      <div class="row">
        <Popup :product="product" :discount="discount"  v-if="showPopup" :class="{ showPopup : showPopup }" v-on:closePopup="closePopupMethod" />
        <Product :product="product" v-for="product in products" :key="product.id"
          v-on:openPopup="openPopupMethod" />
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
        showPopup: false,
        discount: 0
      }
    },
    components: {
      Product,
      Popup
    },
    created() {
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
      openPopupMethod(product,discount) {
        this.product = product
        this.discount = discount
        this.showPopup = true
        $('body').addClass('modal-open')

      },
      closePopupMethod() {
        this.product = {}
        this.showPopup = false
        $('body').removeClass('modal-open')

}
    },
    mounted() {

    }
  }
</script>

<style lang="scss">
@import 'components/sass/style.scss';
</style>

<template>
  <!-- Start Product -->
  <div class="col-xs-12 col-sm-6 col-md-4 col-xl-3 ">
    <div class="Product">
      <!-- Start Product Image -->
      <div class="Product_img">
        <img :src="product.image_url" alt="" class="img-fluid">
        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" fill="currentColor" class="bi bi-heart"
          viewBox="0 0 16 16">
          <path
            d="M8 2.748l-.717-.737C5.6.281 2.514.878 1.4 3.053c-.523 1.023-.641 2.5.314 4.385.92 1.815 2.834 3.989 6.286 6.357 3.452-2.368 5.365-4.542 6.286-6.357.955-1.886.838-3.362.314-4.385C13.486.878 10.4.28 8.717 2.01L8 2.748zM8 15C-7.333 4.868 3.279-3.04 7.824 1.143c.06.055.119.112.176.171a3.12 3.12 0 0 1 .176-.17C12.72-3.042 23.333 4.867 8 15z" />
        </svg>
      </div>
      <!-- End Product image -->
      <!-- Start Product Data -->
      <div class="Product_data">
        <h3> {{product.name}} </h3>
        <p class="shortName"> {{product.brand_value }} </p>
        <ul>
          <li class="price text-left"> {{price.default_formated}} </li>
          <li class="discount text-right" v-if="discount > 0 "><span>-{{discount}} %</span> </li>

          <li class="orginalPrice text-left" v-if="price.default_original_formated"> {{price.default_original_formated}}
          </li>
          <li class="discount text-right" v-if="diff > 0 "> Save {{diff}} {{product.currency}}</li>
        </ul>
        <!-- Button Add To Cart -->
        <button type="button" class="btn btn-primary Add" v-on:click="$emit('openPopup', product, discount)">
          Add
        </button>
      </div>
      <!-- End Product Data -->
    </div>
  </div>
  <!-- End Product -->
</template>

<script>
  export default {
    name: 'Product',
    data() {
      return {
        love: true
      }
    },
    props: {
      product: {
        type: Object,
        required: true
      }
    },
    computed: {
      price() {
        return this.product.price[this.product.currency]
      },
      diff() {
        return this.price.default_original - this.price.default
      },
      discount() {
        return ((this.diff / this.price.default_original) * 100).toFixed()
      }
    }
  }
</script>

 <style lang="scss">
  
</style>
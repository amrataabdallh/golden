<template>
  <!-- Start Modal -->
  <div class="modal fade show" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="overlay" v-on:click="$emit('closePopup')"></div>
    <div class="modal-dialog modal-lg modal-dialog-centered">
      <div class="modal-content">
        <!-- Modal Header -->
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel"> Add item to cart </h5>
          <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"
            v-on:click="$emit('closePopup')">
            <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" fill="currentColor"
              class="bi bi-x-circle-fill" viewBox="0 0 16 16">
              <path d="M16 8A8 8 0 1 1 0 8a8 8 0 0 1 16 0zM5.354 4.646a.5.5 0 1 0-.708.708L7.293 8l-2.647 2.646a.5.5 0 0 0 .708.708L8 8.707l2.646 2.647a.5.5 0 0 0 .708-.708L8.707 8l2.647-2.646a.5.5 0 0 0-.708-.708L8 7.293 5.354 4.646z" />
            </svg>
          </button>

        </div>
        <!-- End Modal Header -->
        <!-- Modal Body -->
        <div class="modal-body">
          <div class="card">
            <div class="row g-0">
              <div class="col-md-4 imgPopup">
                <img :src="product.image_url" alt="" class="img-fluid">
              </div>
              <div class="col-md-8">
                <div class="card-body">
                  <h5 class="card-title">{{product.name}} </h5>
                  <p class="shortName"> {{product.brand_value }} </p>
                  <p class="card-text">{{product.price[product.currency].default_formated}} 
                    <span class="oldPrice">  {{product.price[product.currency].default_original_formated}} </span> 
                       <span class="discount text-right" v-if="discount > 0 "> -{{discount}} % </span>
                    </p>
                 
                  <router-link to="/" tag="a" class="moreDetails"> View Product Details</router-link>
                  <ul class="Size" v-if="product.size_new">
                    <h3>Size </h3>
                    <li v-for="size in product.size_new" :key="size.id" :class="{active: activeSize === size}">
                      <input type="radio" name="size" id="" :value="size" @click="activeSize = size "> {{size}}
                    </li>

                  </ul>
                </div>
              </div>
            </div>
          </div>
        </div>
        <!-- End Modal Body -->
        <div class="modal-footer">
          <button type="button" class="btn btn-secondary close" data-bs-dismiss="modal"
            v-on:click="$emit('closePopup')">Close</button>
          <button type="button" class="btn btn-primary Add" :class="{cart : cart}" @click="addToCart()"> {{ value}}
          </button>
        </div>
      </div>
    </div>
  </div>
  <!-- End Modal -->
</template>

<script>
  export default {
    name: 'Popup',
    data() {
      return {
        value: 'Add to cart',
        cart: false,
        activeSize: null
      }
    },
    methods: {
      addToCart() {
        this.value = 'Item in cart '
        this.cart = true
      }
    },
    props: {
      product: {
        type: Object,
        required: true
      },
      discount:{
        type: Number,
        default: 0,
        required: false 
      }
    },
  }
</script>

<style lang="scss">

</style>
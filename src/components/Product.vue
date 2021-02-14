<template>
  <div id="product">
    <div class="product">
      <div class="product-image">
        <img :src="image" :alt="product" />
      </div>
      <div class="product-info">
        <h1>What I sell: {{ title }}</h1>
        <p>{{ description }}</p>
        <a :href="search + product">Find more things like this!</a>
        <p v-if="inStock >= 10">In Stock</p>
        <p v-else-if="inStock < 10 && inStock > 0">Almost sold out!</p>
        <p v-else :style="{ textDecoration: lineThrough }">Out of Stock</p>
        <p v-show="onSale">{{ printSale }}</p>
        <DetailShippingTabs :details="details" :shipping="shipping" />

        <div
          v-for="(variant, index) in variants"
          :key="variant.id"
          class="color-box"
          :style="{ backgroundColor: variant.color }"
          @mouseover="updateProduct(index)"
        ></div>
        <div>
          <button
            :class="{
              disabledButton: !inStock,
            }"
            v-on:click="addToCart()"
            :disabled="!inStock"
          >
            Add to Cart
          </button>
          <br />
          <button v-on:click="takeFromCart()">Take away from Cart</button>
        </div>

        <ProductTabs :reviews="reviews" />
      </div>
    </div>
  </div>
</template>

<script>
import ProductTabs from '@/components/ProductTabs'
import DetailShippingTabs from '@/components/DetailShippingTabs'
import { eventBus } from './../main'

export default {
  components: { ProductTabs, DetailShippingTabs },
  mounted() {
    eventBus.$on('review-submitted', (productReview) => {
      this.reviews.push(productReview)
    })
  },
  props: {
    premium: {
      type: Boolean,
      required: true,
    },
  },
  data: function () {
    return {
      product: 'Socks',
      brand: 'Vue Mastery',
      description: 'A pair of warm, fuzzy socks.',
      selectedVariant: 0,
      search: 'https://www.google.com/search?q=',

      twoInCart: {
        color: 'cyan',
        backgroundColor: 'pink',
      },
      onSale: true,
      lineThrough: 'line-through',
      cart: 0,
      details: ['80% cotton', '20% polyester', 'Gender Neutral'],
      variants: [
        {
          id: 0,
          color: 'green',
          image: './assets/socks-green.png',
          quantity: 10,
        },
        { id: 1, color: 'blue', image: './assets/socks-blue.jpg', quantity: 5 },
      ],

      sizes: [
        { id: 0, numbers: '32-35' },
        { id: 1, numbers: '36-39' },
      ],
      reviews: [],
    }
  },
  methods: {
    updateProduct(index) {
      this.selectedVariant = index
    },
    addToCart() {
      this.$emit('add-to-cart', this.variants[this.selectedVariant].id)
    },
    takeFromCart() {
      this.$emit('remove-from-cart', this.variants[this.selectedVariant].id)
    },
  },

  computed: {
    title() {
      return this.brand + ' ' + this.product
    },
    image() {
      return this.variants[this.selectedVariant].image
    },
    inStock() {
      return this.variants[this.selectedVariant].quantity
    },
    printSale() {
      return this.brand + ' ' + this.product + ' are on sale!'
    },
    shipping() {
      if (this.premium) return 'free bish'
      else return '$2.99'
    },
  },
}
</script>

<style>
body {
  font-family: tahoma;
  color: #282828;
  margin: 0px;
}

.nav-bar {
  background: linear-gradient(-90deg, #84cf6a, #16c0b0);
  height: 60px;
  margin-bottom: 15px;
}

.product {
  display: flex;
  flex-flow: wrap;
  padding: 1rem;
}

img {
  border: 1px solid #d8d8d8;
  width: 70%;
  margin: 40px;
  box-shadow: 0px 0.5px 1px #d8d8d8;
}

.product-image {
  width: 80%;
}

.product-image,
.product-info {
  margin-top: 10px;
  width: 50%;
}

.color-box {
  width: 40px;
  height: 40px;
  margin-top: 5px;
}

.cart {
  margin-right: 25px;
  float: right;
  border: 1px solid #d8d8d8;
  padding: 5px 20px;
}

button {
  margin-top: 30px;
  border: none;
  background-color: #1e95ea;
  color: white;
  height: 40px;
  width: 100px;
  font-size: 14px;
}

.disabledButton {
  background-color: #d8d8d8;
}

.review-form {
  width: 400px;
  padding: 20px;
  margin: 40px;
  border: 1px solid #d8d8d8;
}

input {
  width: 100%;
  height: 25px;
  margin-bottom: 20px;
}

textarea {
  width: 100%;
  height: 60px;
}

.tab {
  margin-left: 10px;
  cursor: pointer;
}

.activeTab {
  color: #16c0b0;
  text-decoration: underline;
}
</style>

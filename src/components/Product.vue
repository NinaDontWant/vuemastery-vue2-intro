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

        <ProductDetails :details="details" />
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
              badassBackground: makeBadass,
            }"
            v-on:click="addToCart()"
            :disabled="!inStock"
          >
            Add to Cart
          </button>
          <br />
          <button v-on:click="takeFromCart()">Take away from Cart</button>
        </div>
        <div class="cart">Cart({{ cart }})</div>

        <p>Shipping costs: {{ shipping }}</p>
      </div>
    </div>
  </div>
</template>

<script>
import ProductDetails from '@/components/ProductDetails'
export default {
  components: { ProductDetails },
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

      makeBadass: false,
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
        { id: 1, color: 'blue', image: './assets/socks-blue.jpg', quantity: 0 },
      ],

      sizes: [
        { id: 0, numbers: '32-35' },
        { id: 1, numbers: '36-39' },
      ],
    }
  },
  methods: {
    updateProduct(index) {
      this.selectedVariant = index
    },
    addToCart() {
      this.cart++
      this.makeBadass = this.cart === 3
    },
    takeFromCart() {
      if (this.cart > 0) this.cart--
      this.makeBadass = this.cart === 3
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
#product {
  /*background-color: lightblue;*/
}
</style>

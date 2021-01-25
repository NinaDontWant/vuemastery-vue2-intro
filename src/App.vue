<template>
  <div>
    <div class="nav-bar"></div>
    <div id="app">
      <div class="product">
        <div class="product-image">
          <img :src="image" :alt="product" />
        </div>
        <div class="product-info">
          <h1>What I sell: {{ title }}</h1>
          <p>{{ description }}</p>
          <a :href="search + product">Find more things like this!</a>
          <p v-if="variants[selectedVariant].quantity >= 10">In Stock</p>
          <p
            v-else-if="
              variants[selectedVariant].quantity < 10 &&
              variants[selectedVariant].quantity > 0
            "
          >
            Almost sold out!
          </p>
          <p v-else :style="{ textDecoration: lineThrough }">Out of Stock</p>
          <p v-show="onSale">{{ printSale }}</p>

          <ul>
            <li v-for="detail in details" :key="details.indexOf(detail)">
              {{ detail }}
            </li>
          </ul>
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
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
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
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

body {
  font-family: tahoma, serif;
  color: #282828;
  margin: 0;
}

.nav-bar {
  background: linear-gradient(-90deg, #84cf6a, #16c0b0);
  height: 60px;
  margin-bottom: 15px;
}

.product {
  display: flex;
}

img {
  border: 1px solid #d8d8d8;
  width: 70%;
  margin: 40px;
  box-shadow: 0 1px 1px #d8d8d8;
}

.product-image {
  flex-basis: 700px;
}

.product-info {
  margin-top: 10px;
  flex-basis: 500px;
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

.badassBackground {
  background-color: black;
}

.review-form {
  width: 30%;
  padding: 20px;
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
</style>

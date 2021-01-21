<template>
  <div>
    <div class="nav-bar"></div>
    <div id="app">
      <div class="product">
        <div class="product-image">
          <img :src="image" :alt="product" />
        </div>
        <div class="product-info">
          <h1>What I sell: {{ product }}</h1>
          <p>{{ description }}</p>
          <a :href="search + product">Find more things like this!</a>
          <p v-if="inventory > 10">In Stock</p>
          <p v-else-if="inventory <= 10 && inventory > 0">Almost sold out!</p>
          <p v-else>Out of Stock</p>
          <p v-show="onSale">On Sale! :D</p>

          <ul>
            <li v-for="detail in details" :key="details.indexOf(detail)">
              {{ detail }}
            </li>
          </ul>
          <div v-for="variant in variants" :key="variant.id">
            <p @ mouseover="updateProduct(variant.image)">
              {{ variant.color }}
            </p>
          </div>
          <div>
            <button v-on:click="addToCart()">Add to Cart</button>
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
      description: 'A pair of warm, fuzzy socks.',
      image: './assets/socks-green.png',
      search: 'https://www.google.com/search?q=',
      inStock: true,
      inventory: 0,
      onSale: true,
      cart: 0,
      details: ['80% cotton', '20% polyester', 'Gender Neutral'],
      variants: [
        { id: 0, color: 'green', image: './assets/socks-green.png' },
        { id: 1, color: 'blue', image: './assets/socks-blue.jpg' },
      ],

      sizes: [
        { id: 0, numbers: '32-35' },
        { id: 1, numbers: '36-39' },
      ],
    }
  },
  methods: {
    updateProduct(variantImage) {
      this.image = variantImage
    },
    addToCart() {
      this.cart++
    },
    takeFromCart() {
      if (this.cart > 0) this.cart--
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
}

img {
  border: 1px solid #d8d8d8;
  width: 70%;
  margin: 40px;
  box-shadow: 0px 0.5px 1px #d8d8d8;
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

.disabledButton {
  background-color: #d8d8d8;
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

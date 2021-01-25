<template>
  <div>
    <div class="nav-bar"></div>
    <div id="app">
      <div class="product">
        <div class="product-image">
          <img :src="image" :alt="product" />
        </div>

        <div class="product-info">
          <h1>What I sell: {{title}}</h1>
          <p>{{description}}</p>
          <a :href="search+product">Find more things like this!</a>
          <p v-if="inStock>10">In Stock</p>
          <p v-else-if="inStock<=10&&inStock>0">Almost sold out!</p>
          <p v-else :class="{outOfStock: !inStock}">Out of Stock</p>
          <p v-show="onSale">On Sale! :D</p>

          <ul>
            <li v-for="detail in details" :key="details.indexOf(detail)">{{detail}}</li>
          </ul>

          <ul>
            Sizes:
            <li v-for="size in sizes" :key="size.id">{{size.numbers}}</li>
          </ul>
          <div
            class="color-box"
            v-for="(variant, index) in variants"
            :key="variant.id"
            :style="{backgroundColor: variant.color}"
            @mouseover="updateProduct(index)"
          ></div>
        </div>
        <div class="cart">
          <p>Cart({{cart}})</p>
          <button
            @click="addToCart"
            :disabled="!inStock"
            :class="{disabledButton: !inStock}"
          >Add to Cart</button>
          <button
            @click="removeFromCart"
            :disabled="!cart"
            :class="{disabledButton: !cart}"
          >Remove from Cart</button>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  name: "app",
  data: function() {
    return {
      product: "Socks",
      selectedVariant: 0,
      brand: "Vue Mastery",
      description: "A pair of warm, fuzzy socks.",
      search: "https://www.google.com/search?q=",
      onSale: true,
      details: ["80% cotton", "20% polyester", "Gender-neutral"],
      variants: [
        {
          id: 2234,
          color: "green",
          image: "./assets/socks-green.png",
          inventory: 10
        },
        {
          id: 2235,
          color: "blue",
          image: "./assets/vmSocks-blue-onWhite.jpg",
          inventory: 0
        }
      ],
      sizes: [
        { id: 0, numbers: "33-35" },
        { id: 1, numbers: "36-38" },
        { id: 2, numbers: "39-41" },
        { id: 3, numbers: "42-44" }
      ],
      cart: 0
    };
  },
  methods: {
    addToCart: function() {
      this.cart += 1;
    },
    removeFromCart: function() {
      this.cart -= 1;
    },
    updateProduct(index) {
      this.selectedVariant = index;
      console.log(index)
    }
  },
  computed: {
    title() {
      if (this.onSale) return this.brand + " " + this.product;
      else return "we don't have anything for you";
    },
    image() {
      return this.variants[this.selectedVariant].image
    },
    inStock(){
      return this.variants[this.selectedVariant].inventory
    }
  }
};
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

.outOfStock {
  text-decoration: line-through;
}
</style>

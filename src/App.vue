<template>
  <div>
    <div class="nav-bar"></div>
    <div id="app">
      <div class="cart">Cart({{ cart.length }})</div>
      <Product
        @add-to-cart="addToCart"
        @remove-from-cart="removeFromCart"
        :premium="premium"
      />
    </div>
  </div>
</template>

<script>
import Product from './components/Product'

export default {
  name: 'app',
  components: { Product },
  data: () => {
    return {
      premium: true,
      cart: [],
    }
  },
  methods: {
    addToCart(id) {
      this.cart.push(id)
    },
    removeFromCart(id) {
      for (let i = 0; i < this.cart.length; i++) {
        const cartId = this.cart[i]
        if (cartId === id) {
          this.cart.splice(i, 1)
          break
        }
      }
    },
  },
}
</script>

<style></style>

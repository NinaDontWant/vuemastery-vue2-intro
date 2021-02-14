<template>
	<div>
		<div class="nav-bar"></div>
		<div id="app">
			<div class="cart">
				<p>Cart({{ cart.length }})</p>
			</div>
			<br />
			<Product
				:premium="premium"
				@add-to-cart="incrementCart"
				@remove-from-cart="decrementCart"
			/>
			<Product2
				:premium="!premium"
				@add-to-cart="incrementCart"
				@remove-from-cart="decrementCart"
			/>
		</div>
	</div>
</template>

<script>
import Product from "./components/Product";
import Product2 from "./components/Product2";

export default {
	name: "app",
	components: { Product, Product2 },
	data: function() {
		return {
			premium: true,
			cart: [],
		};
	},
	methods: {
		incrementCart(id) {
			this.cart.push(id);
			console.log(this.cart);
		},
		decrementCart(id) {
			//this.cart.sort();
			for (var i = 0; i < this.cart.length; i++) {
				if (this.cart[i] === id) {
					this.cart.splice(i, 1);
					break;
				}
			}
			console.log(this.cart);
		},
	},
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
	flex-basis: 700px;
}

.product-image,
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
	margin: 20px 5px;
	border: none;
	background-color: #1e95ea;
	color: white;
	height: 40px;
	width: 100px;
	font-size: 14px;
	padding: 5px 20px;

}

.disabledButton {
	background-color: #d8d8d8;
}

.review-form {
	width: 30%;
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

.outOfStock {
	text-decoration: line-through;
}

.tabs {
	margin-left: 20px;
	cursor: pointer;
}

.activeTab {
	color: #16c0b0;
	text-decoration: underline;
}
</style>

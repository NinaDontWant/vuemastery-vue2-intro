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
				<p v-if="inStock > 10">In Stock</p>
				<p v-else-if="inStock <= 10 && inStock > 0">Almost sold out!</p>
				<p v-else :class="{ outOfStock: !inStock }">Out of Stock</p>
				<p v-show="onSale">On Sale! :D</p>
				
				<p>Shipping: {{ shipping }}</p>
				
				<ProductDetails />

				<ul>
					Sizes:
					<li v-for="size in sizes" :key="size.id">{{ size.numbers }}</li>
				</ul>
				<div
					class="color-box"
					v-for="(variant, index) in variants"
					:key="variant.id"
					:style="{ backgroundColor: variant.color }"
					@mouseover="updateProduct(index)"
				></div>
			</div>
			<ProductTabs :reviews="reviews" />
			<!-- <div>
				<h2>Reviews</h2>
				<p v-if="!reviews.length">There are no reviews yet.</p>
				<ul>
					<li v-for="review in reviews" :key="review.id">
						<p>{{ review.name }}</p>
						<p>Rating: {{ review.rating }}</p>
						<p>{{ review.review }}</p>
						<p>Would recommend: {{ review.recommend }}</p>
					</li>
				</ul>
			</div>
			<ProductReview @review-submitted="addReview" /> -->
			<div class="buttons">
				<button
					@click="addToCart"
					:disabled="!inStock"
					:class="{ disabledButton: !inStock }"
				>
					Add to Cart
				</button>
				<button @click="removeFromCart">Remove from Cart</button>
				<!--    potentially also within the button description, but with reference to the cart in the parent app.vue
          :disabled="!cart"
          :class="{disabledButton: !cart}" -->
			</div>
		</div>
	</div>
</template>

<script>
import ProductDetails from "./ProductDetails";
// import ProductReview from "./ProductReview";
import ProductTabs from "./ProductTabs";
import { eventBus } from "../main";

// Productreview used to be in the components two lines down.
export default {
	components: { ProductDetails, ProductTabs },
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
					inventory: 10,
				},
				{
					id: 2235,
					color: "blue",
					image: "./assets/vmSocks-blue-onWhite.jpg",
					inventory: 4,
				},
			],
			sizes: [
				{ id: 0, numbers: "33-35" },
				{ id: 1, numbers: "36-38" },
				{ id: 2, numbers: "39-41" },
				{ id: 3, numbers: "42-44" },
			],
			// cart: 0
			reviews: [],
		};
	},
	methods: {
		addToCart: function() {
			this.$emit("add-to-cart", this.variants[this.selectedVariant].id);
		},
		removeFromCart: function() {
			this.$emit("remove-from-cart", this.variants[this.selectedVariant].id);
		},
		updateProduct(index) {
			this.selectedVariant = index;
			console.log(index);
		},
		// addReview(productReview) {
		// 	this.reviews.push(productReview);
		// },
		// created() {
		// 	eventBus.$on("review-submitted", (productReview) => {
		// 		this.reviews.push(productReview);
		// 	});
		// },
	},
	computed: {
		title() {
			if (this.onSale) return this.brand + " " + this.product;
			else return "we don't have anything for you";
		},
		image() {
			return this.variants[this.selectedVariant].image;
		},
		inStock() {
			return this.variants[this.selectedVariant].inventory;
		},
		shipping() {
			if (this.premium) return "free";
			else return "$2,99";
		},
	},
	props: {
		premium: {
			type: Boolean,
			required: true,
		},
		
	},
	mounted() {
		eventBus.$on("review-submitted", (productReview) => {
			this.reviews.push(productReview);
		});
	},
};
</script>

<style></style>

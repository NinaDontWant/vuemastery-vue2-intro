<template>
	<div>
		<span
			:class="{ activeTab: selectedTab === tab }"
			v-for="(tab, index) in tabs"
			:key="index"
			@click="selectedTab = tab"
			>{{ tab }}
		</span>

		<div v-show="selectedTab === 'Reviews'">
			<p v-if="!reviews.length">There are no reviews yet.</p>
			<ul v-else>
				<li v-for="(review, index) in reviews" :key="index">
					<p>{{ review.name }}</p>
					<p>{{ review.review }}</p>
					<p>Rating: {{ review.rating }}</p>
					<p>Would recommend: {{ review.recommend }}</p>
				</li>
			</ul>
		</div>
		<div v-show="selectedTab === 'Make a Review'">
			<ProductReview @review-submitted="addReview" />
		</div>
	</div>
</template>

<script>
import ProductReview from "./ProductReview";

export default {
	components: { ProductReview },
	data() {
		return {
			tabs: ["Reviews", "Make a Review"],
			selectedTab: "Reviews",
			// reviews: [],
		};
	},
	methods: {
		addReview(productReview) {
			this.reviews.push(productReview);
		},
    },
    props:{
        reviews: {
        type: Array,
        required: false
      }
    }
};
</script>

<style></style>

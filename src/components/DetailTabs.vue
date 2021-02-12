<template>
	<div>
		<span
			:class="{ activeTab: selectedTab === tab }"
			v-for="(tab, index) in tabs"
			:key="index"
			@click="selectedTab = tab"
			>{{ tab }}
		</span>

		<div v-show="selectedTab === 'Details'">
			<ProductDetails />
		</div>

		<div v-show="selectedTab === 'Shipping'">
			<p>
				Shipping:
				{{ shipping }}
			</p>
		</div>
	</div>
</template>

<script>
import ProductDetails from "./ProductDetails";
export default {
	components: { ProductDetails },
	data() {
		return {
			tabs: ["Details", "Shipping"],
			selectedTab: "Shipping",
		};
	},
    computed: {
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
};
</script>

<style></style>

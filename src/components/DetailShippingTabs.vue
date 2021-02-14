<template>
  <div>
    <h4>
      <span
        @click="selectedTab = tab"
        class="tab"
        :class="{ activeTab: selectedTab === tab }"
        v-for="(tab, index) in tabs"
        :key="index"
      >
        {{ tab }}
      </span>
    </h4>
    <ProductDetails :details="details" v-show="selectedTab === 'Details'" />
    <p v-show="selectedTab === 'Shipping'">Shipping costs: {{ shipping }}</p>
  </div>
</template>

<script>
import ProductDetails from '@/components/ProductDetails'

export default {
  components: {
    ProductDetails,
  },
  props: {
    details: {
      type: Array,
      required: true,
    },
    shipping: {
      type: String,
      required: true,
    },
  },
  data() {
    return {
      selectedTab: 'Details',
      tabs: ['Details', 'Shipping'],
    }
  },
}
</script>

<style></style>

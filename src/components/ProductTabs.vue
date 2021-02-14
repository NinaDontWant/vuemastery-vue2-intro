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
    <div v-show="selectedTab == 'Reviews'">
      <p v-if="!reviews.length">There are no reviews yet</p>
      <ul>
        <li :key="review.name" v-for="review in reviews">
          <p>{{ review.name }}</p>
          <p>Rating: {{ review.rating }}</p>
          <p>{{ review.review }}</p>
        </li>
      </ul>
    </div>
    <ProductReview v-show="selectedTab == 'Make a Review'" />
  </div>
</template>

<script>
import ProductReview from '@/components/ProductReview'

export default {
  components: {
    ProductReview,
  },
  props: {
    reviews: {
      type: Array,
      required: false,
    },
  },
  data() {
    return {
      tabs: ['Reviews', 'Make a Review'],
      selectedTab: '',
    }
  },
}
</script>

<style></style>

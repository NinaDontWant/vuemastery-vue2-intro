<template>
  <div>
    <form class="review-form" @submit.prevent="onSubmit">
      <p>
        <label for="name">Name:</label>
        <input id="name" v-model="name" placeholder="name" />
      </p>

      <p>
        <label for="review">Review:</label>
        <textarea id="review" v-model="review"></textarea>
      </p>

      <p>
        <label for="rating">Rating:</label>
        <select id="rating" v-model.number="rating">
          <option>5</option>
          <option>4</option>
          <option>3</option>
          <option>2</option>
          <option>1</option>
        </select>
      </p>
      <p>
        Would you recommend this product?<br />
        <label for="yes">Yes</label>
        <input
          v-model="recommend"
          type="radio"
          id="yes"
          name="recommend-product"
          value="true"
        />
        <label for="no">No</label>
        <input
          v-model="recommend"
          type="radio"
          id="no"
          name="recommend-product"
          value="false"
        />
      </p>
      <p>
        <input type="submit" value="Submit" />
      </p>
      <div v-if="errors.length">
        <b>Please correct the following error(s):</b>
      </div>
      <ul>
        <li :key="error" v-for="error in errors">{{ error }}</li>
      </ul>
    </form>
  </div>
</template>

<script>
export default {
  name: 'ProductReview',
  data() {
    return {
      name: null,
      review: null,
      rating: null,
      errors: [],
      recommend: null,
    }
  },
  methods: {
    onSubmit() {
      if (this.name && this.review && this.rating) {
        this.errors.splice(0, this.errors.length)
        let productReview = {
          name: this.name,
          review: this.review,
          rating: Number(this.rating),
          recommend: this.recommend,
        }
        this.$emit('review-submitted', productReview)
        this.name = null
        this.review = null
        this.rating = null
        this.recommend = null
      } else {
        this.errors.splice(0, this.errors.length)
        if (!this.name) this.errors.push('Name required.')
        if (!this.review) this.errors.push('Review required.')
        if (!this.rating) this.errors.push('Rating required.')
        if (!this.recommend) this.errors.push('Recommendation required.')
      }
    },
  },
}
</script>

<style></style>

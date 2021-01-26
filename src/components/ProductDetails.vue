<template>
  <div id="product-details">
    <ul>
      <li v-for="detail in details" :key="details.indexOf(detail)">
        {{ detail }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: {
    details: {
      type: Array,
      required: true,
    },
  },
}
</script>

<style></style>

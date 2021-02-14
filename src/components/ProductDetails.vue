<template>
  <ul>
    <li v-for="detail in details" :key="details.indexOf(detail)">{{detail}}</li>
  </ul>
</template>


<script>
export default {
    data: function() {
        return {
        details: ["80% cotton", "20% polyester", "Gender-neutral"],
        }
    }
};
</script>


<style>
</style>
<template>
  <div class="discount">
    <h5>지금 결제하면 {{ discount }}% 할인</h5>
  </div>
</template>

<script>
export default {
  name: "DiscountVue",
  props: {
    discount: Number,
  },
};
</script>

<style scoped>
.discount {
  background-color: #eee;
  padding: 20px;
  margin: 10px 0;
  border-radius: 5px;
  text-align: center;
}
</style>
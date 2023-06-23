<template>
  <div>
    <img :src="item.image" @click="open" class="room-img" />
    <h4>{{ item.title }}</h4>
    <p>{{ item.price.toLocaleString("ko-KR") }} 원</p>
    <button @click="increase">허위매물신고</button>
    <span class="fakeCount">신고수 : {{ item.fakeReport }}</span>
  </div>
</template>

<script>
export default {
  name: "CardVue",
  props: {
    item: Object,
  },
  methods: {
    open() {
      this.$emit("open");
    },
    increase() {
      this.$emit("increase");
    },
  },
};
</script>

<style scoped>
.fakeCount {
  display: inline-block;
  margin-left: 20px;
}
.room-img {
  width: 100%;
  margin-top: 40px;
}
</style>
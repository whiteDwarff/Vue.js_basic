<template>
  <div class="black-bg" v-if="isModalState">
    <div class="white-bg">
      <button @click="close" class="button">
        <font-awesome-icon :icon="['fas', 'xmark-large']" />
      </button>
      <img :src="item.image" class="room-img-comp" />
      <h4>{{ item.title }}</h4>
      <p>{{ item.content }}</p>
      <!-- v-model="" 사용자가 입력한 데이터를 data(){} 내 변수에 저장  -->
      <!-- <input v-model.number="month" type="text" /> -->
      <input type="range" min="1" max="12" v-model.number="month" />
      <p>{{ month }}개월 : {{ returnPrice(month, item.price) }} 원</p>
    </div>
  </div>
</template>

<script>
export default {
  name: "ModalVue",
  data() {
    return {
      month: 3,
    };
  },
  props: {
    item: Object,
    index: Number,
    isModalState: Boolean,
  },
  // 실시간으로 입력받은 input의 데이터를 감시, 데이터가 바뀔 떄 마다 함수 실행
  watch: {
    // month를 감시하는 메소드(메서드 이름과 데이터의 이름을 동일하게 사용)
    month(data) {
      if (isNaN(data)) {
        alert("숫자만 입력해주새요.");
        this.month = 3;
      } else if (data > 12) {
        alert("최대 12개월까지 선택가능합니다.");
        this.month = 3;
      }
    },
  },
  methods: {
    close() {
      this.$emit("close");
      this.month = 1;
    },
    returnPrice(month, price) {
      let sum = month * price;
      return sum.toLocaleString("ko-KR");
    },
  },
  // 컴포넌트의 재랜더링 시 발생하는 life cycle
  // beforeUpdate는 update되기 바로 직전 실행시킨다.
  beforeUpdate() {},
};
</script>

<style scoped>
.black-bg {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  top: 0;
  left: 0;
}
.white-bg {
  width: 80%;
  height: 95%;
  background-color: #fff;
  border-radius: 8px;
  margin: auto;
  padding: 20px;
  text-align: center;
}
.button {
  display: block;
  margin-left: auto;
}
.room-img-comp {
  width: 90%;
}
</style>
<template>
  <div>
    <!-- vue의  내장된 애니메이션 태그, name값은 작명 가능하다. css에서 부가 설정!! -->
    <Transition name="fade">
      <ModalVue
        :item="oneRooms[index]"
        :isModalState="isModalState"
        @close="modalClose"
      />
    </Transition>
    <div class="menu">
      <a v-for="(item, i) in menu" :key="i">{{ item }}</a>
    </div>
    <Transition name="fade">
      <DiscountVue v-if="showDiscount" :discount="discount" />
    </Transition>
    <select v-model="selectValue" @change="dataSort" id="select-bar">
      <option value="0">기본순</option>
      <option value="1">가격낮은순</option>
      <option value="2">가격높은순</option>
      <option value="3">이름빠른순</option>
      <option value="4">이름느린순</option>
    </select>
    <CardVue
      v-for="(item, i) in oneRooms"
      :key="i"
      :item="item"
      @open="modalOpen(i)"
      @increase="increase(i)"
      class="card"
    />
  </div>
</template>

<script>
import oneRooms from "./assets/data.js";
import DiscountVue from "./components/DiscountVue";
import ModalVue from "./components/ModalVue";
import CardVue from "./components/CardVue";

export default {
  name: "App",
  data() {
    return {
      menu: ["Home", "Product", "About"],
      showDiscount: true,
      discount: 30,
      isModalState: false,
      index: 0,
      selectValue: 0,
      orgOneRooms: [...oneRooms],
      oneRooms,
    };
  },
  methods: {
    increase(i) {
      this.oneRooms[i].fakeReport += 1;
    },
    modalOpen(i) {
      this.isModalState = !this.isModalState;
      this.index = i;
    },
    modalClose() {
      this.isModalState = !this.isModalState;
    },
    dataSort() {
      let option = this.selectValue;
      if (option == 0) {
        this.oneRooms = [...this.orgOneRooms];
      } else if (option == 1) {
        this.oneRooms.sort(function (a, b) {
          return a.price - b.price;
        });
      } else if (option == 2) {
        this.oneRooms.sort(function (a, b) {
          return b.price - a.price;
        });
      } else if (option == 3) {
        this.oneRooms.sort(function (a, b) {
          if (a.title < b.title) return -1;
        });
      } else if (option == 4) {
        this.oneRooms.sort(function (a, b) {
          if (a.title > b.title) return -1;
        });
      }
    },
  },
  // html 생성 전, 데이터만 존재할 때
  created() {},
  // html과 data가 생성된 후
  mounted() {
    setInterval(() => {
      this.discount -= 1;
      if (this.discount == 0) {
        this.showDiscount = !this.showDiscount;
        return;
      }
    }, 1000);
  },
  components: {
    DiscountVue,
    ModalVue,
    CardVue,
  },
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  text-decoration: none;
}
.menu {
  background-color: darkslateblue;
  padding: 15px;
  border-radius: 5px;
  text-align: center;
}
.menu a {
  color: #fff;
  padding: 30px;
}
#select-bar {
  display: block;
  padding-right: 10px;
  margin-left: auto;
}
.card {
  text-align: center;
}
/* -------------- Transition의 css 구성 --------------- */
/* 시작 */
.fade-enter-from {
  opacity: 0;
  /* transform: translateY(-1000px); */
}
.fade-enter-active {
  transition: 0.4s ease-out;
}
.fade-enter-to {
  opacity: 1;
}

/* 끝 */
.fade-leave-from {
  opacity: 1;
  /* transform: translateY(0); */
}
.fade-leave-active {
  transition: 0.4s ease-out;
}
.fade-leave-to {
  opacity: 0;
}
</style>

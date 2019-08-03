<template>
  <div>
    <button
      v-for="(tab,index) in item"
      :key="index"
      @click="choose(tab)"
      :class="tab.isActive?classA:''"
    >{{tab.con}}</button>

    <chuan></chuan>
  </div>
</template>
<script>
import chuan from "../../components/chuan";
export default {
  data() {
    return {
      item: [
        { con: "羽毛球", isActive: false },
        { con: "篮球", isActive: false },
        { con: "乒乓球", isActive: false },
        { con: "排球", isActive: false }
      ],
      classA: "classA",
      isActive: false,
      index: 54587
    };
  },
  components: {
    chuan
  },
  methods: {
    choose(tab) {
      tab.isActive = !tab.isActive;
    }
  }
};
</script>

<style>
.classA {
  background: RED;
}
</style>

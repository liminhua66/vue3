<template>
  <h2>{{ count }}</h2>
  <p>name:{{ user.name }}</p>
  <p>age:{{ user.age }}</p>
  <p>cars:{{ user.cars }}</p>
  <hr />
  <button @click="updateCount">更新数据</button>
</template>

<script>
import { defineComponent, reactive, ref } from "vue";
export default defineComponent({
  name: "App",
  setup() {
    const obj = {
      name: "小明",
      age: 18,
      cars: ["BWM", "MB", "AUDI"],
    };
    const user = reactive(obj);
    const count = ref(1);
    const updateCount = () => {
      count.value++;
      user.age += "==";
      user.cars.push("zh");
    };
    return {
      count,
      user,
      updateCount,
    };
  },
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

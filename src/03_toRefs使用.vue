<template>
  <h2>toRefs使用</h2>
  <h3>name:{{ state.name }}</h3>
  <h3>age:{{ state.age }}</h3>

  <h3>name2:{{ name2 }}</h3>
  <h3>age2:{{ age2 }}</h3>
</template>

<script>
import { defineComponent, reactive, toRefs } from "vue";

function useFeature() {
  const state2 = reactive({
    name2: "aaa",
    age2: 18,
  });
  return {
    ...toRefs(state2),
  };
}
export default defineComponent({
  name: "app",
  setup() {
    const state = reactive({
      name: "aaa",
      age: 18,
    });
    // const { name, age } = toRefs(state);
    const { name2, age2 } = useFeature();
    // 定时器
    setInterval(() => {
      name2.value += "===";
    }, 1000);
    return {
      state,
      // ...state2,
      name2,
      age2,
    };
  },
});
</script>

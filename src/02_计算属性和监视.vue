<template>
  <h2>computed and watch</h2>
  <fieldset>
    <legend>姓名操作</legend>
    姓氏：<input
      type="text"
      placeholder="请输入姓氏"
      v-model="user.lastName"
    /><br />
    名字：<input
      type="text"
      placeholder="请输入名字"
      v-model="user.firstName"
    /><br />
  </fieldset>
  <fieldset>
    <legend>计算属性和监视</legend>
    姓名：<input type="text" placeholder="显示姓名" v-model="fullName" /><br />
    姓名：<input type="text" placeholder="显示姓名" v-model="fullName2" /><br />
    姓名：<input type="text" placeholder="显示姓名" v-model="fullName3" /><br />
  </fieldset>
</template>
<script>
import {
  computed,
  defineComponent,
  reactive,
  ref,
  watch,
  watchEffect,
} from "@vue/runtime-core";

export default defineComponent({
  name: "app",
  setup() {
    const user = reactive({
      firstName: "三",
      lastName: "张",
    });
    const fullName = computed(() => {
      return user.lastName + "_" + user.firstName;
    });
    const fullName2 = computed({
      get() {
        return user.lastName + "_" + user.firstName;
      },
      set(val) {
        // console.log(val);
        user.lastName = val.split("_")[0];
        user.firstName = val.split("_")[1];
      },
    });
    const fullName3 = ref("");
    watch(
      user,
      ({ firstName, lastName }) => {
        fullName3.value = lastName + "_" + firstName;
      },
      { immediate: true }
    );
    // watchEffect(() => {
    //   fullName3.value = user.lastName + "_" + user.firstName;
    // });
    watchEffect(() => {
      user.lastName = fullName3.value.split("_")[0];
      user.firstName = fullName3.value.split("_")[1];
    });
    return {
      user,
      fullName,
      fullName2,
      fullName3,
    };
  },
});
</script>
<style lang=""></style>

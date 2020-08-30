<template>
  <div>
    <button @click="handleClick">click</button>
    <p>count : {{ count }}</p>
    <p>state : {{ state.time }}</p>
    <p>state2 : {{ state2.value }}</p>
    <p>double : {{ double }}</p>
  </div>
</template>

<script>
import { ref, reactive, readonly, computed, watch, onMounted } from "vue";
export default {
  setup() {
    // 一、创建响应式对像方式
    // 共3点 ref、reactive、readonly
    // ref 是值类型包装器
    const count = ref(0);
    console.log(count);

    // reactive 是引用类型包装器
    const state = reactive({ time: 0 });
    console.log(state);

    // readonly 只读包装器包装内容与 reactive 相同
    const state2 = readonly({ value: 0 });
    console.log(state2);

    const handleClick = () => {
      count.value++;
      state.time++;
    };

    // 二、响应式系统Api
    // 1.computed 计算属性
    const double = computed(() => {
      return count.value * 2;
    });

    // 2.watch 监听属性，以监听 double 值为例, value是回调函数传来的值
    watch(double, (value) => {
      console.log(value);
    });

    // 三、生命周期
    // 1.onMounted
    onMounted(() => {
      console.log("mounted");
    });

    return {
      double,
      count,
      state,
      state2,
      handleClick,
    };
  },
};
</script>

<style>

p {
  font-size: 20px;
}

</style>
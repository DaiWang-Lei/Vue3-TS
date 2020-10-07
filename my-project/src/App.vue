<template>
  <div>
    <img alt="Vue logo" src="./assets/logo.png" />
    <h1>欢迎光临罗卜达小商店</h1>
    <div>请选择你喜欢的一种食物</div>
    <div>
      <button v-for="(item, i) in foods" :key="i" @click="selectFoodFun(i)">
        {{ item }}
      </button>
    </div>
    <div>哇哦，你喜欢的是【{{ selectFood }}】啊！</div>
    <h1>你最喜欢那条水系？</h1>
    <div>
      <button v-for="(item, i) in waters" :key="i" @click="selectWaterFun(i)">
        {{ item }}
      </button>
    </div>
    <div>哇哦，你喜欢的是【{{ selectWater }}】啊！</div>
  </div>
</template>

<script lang="ts">
import {
  defineComponent,
  ref,
  reactive,
  toRefs,
  onBeforeMount,
  onMounted,
  onUnmounted,
  onBeforeUpdate,
  onUpdated,
  onRenderTracked,
  onRenderTriggered,
} from "vue";

// toRefs形式，所需的接口限制
interface DataProp {
  waters: string[];
  selectWater: string;
  selectWaterFun: (i: number) => void;
}
export default defineComponent({
  name: "App",
  setup() {
    // ref形式
    const foods = ref(["水果", "饮料", "零食"]);
    const selectFood = ref("");
    const selectFoodFun = (i: number) => {
      selectFood.value = foods.value[i];
    };

    // reactive形式，搭配toRefs效果更佳
    const data: DataProp = reactive({
      waters: ["长江", "黄河", "黄海"],
      selectWater: "",
      selectWaterFun: (i: number) => {
        data.selectWater = data.waters[i];
      },
    });
    const refData = toRefs(data);
    console.log("1-开始创建组件-----setup");
    onBeforeMount(() => {
      console.log("2-组件挂在到页面之前执行-----onBeforeMount");
    });
    onMounted(() => {
      console.log("3-组件挂载到页面之后执行-----onMounted");
    });
    onBeforeUpdate(() => {
      console.log("4-组件更新之前执行-----onBeforeUpdate");
    });
    onUpdated(() => {
      console.log("5-组件更新之后执行-----onUpdated");
    });
    // 跟踪页面所有的响应式变化
    // onRenderTracked((e) => {
    //   console.log("状态跟踪钩子函数");
    //   console.log(e);
    // });
    onRenderTriggered((e) => {
      console.log("状态跟踪钩子函数------->");
      console.log(e);
    });

    return {
      foods,
      selectFood,
      selectFoodFun,

      // toRefs形式
      ...refData,
    };
  },
  // Vue2的生命周期
  // beforeCreate(){
  //   console.log('1.1-组件创建之前执行*****beforeCreate')
  // },
  // beforeMount() {
  //   console.log('2.1-组件挂载到页面之前执行******beforeMount')
  // },
  // mounted(){
  //   console.log('3.1-组件挂载到页面之后执行*****mounted')
  // },
  // beforeUpdate() {
  //   console.log('4.1-组件更新之前执行******beforeUpdate')
  // },
  // updated(){
  //   console.log('5.1-组件更新之后执行*****updated')
  // }
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

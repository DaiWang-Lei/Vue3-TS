<template>
  <div>
     <h1>欢迎光临罗卜达小商店</h1>
     <div>随机出现一张照片</div>
  </div>
</template>

<script lang="ts">
    
import {
  defineComponent,
  ref,
  reactive,
  toRefs,
  watch,
} from "vue";
import { nowTime, getNowTime } from "./hooks/useNowTime";

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

    const overText = ref("罗卜大");
    const overAction = () => {
      overText.value = overText.value + "  |  选择完成";
      //   document.title = overText.value;
    };
    const data: DataProp = reactive({
      waters: ["长江", "黄河", "黄海"],
      selectWater: "",
      selectWaterFun: (i: number) => {
        data.selectWater = data.waters[i];
      },
    });
    const refData = toRefs(data);
    // 箭头函数是seter的方式，
    watch([overText, () => data.selectWater], (newValue, oldValue) => {
      console.log(`new---->${newValue}`);
      console.log(`old---->${oldValue}`);
      document.title = newValue[0];
    });
   
    return {
      foods,
      selectFood,
      selectFoodFun,
      overText,
      overAction,
      nowTime,
      getNowTime,
      // toRefs形式
      ...refData,
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

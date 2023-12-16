<template>
  <div>{{ msg.name }} {{ msg.age }}</div>
  <hr>
  <button @click="change">修改</button>
</template>
    
<script setup lang='ts'>
// 导入响应式数据 ref 模块
import { ref, reactive } from 'vue';
// 导入 Ref 类型声明
import { Ref, isRef } from 'vue';

type MsgType = {
  name: string;
  age: number;
}

// const msg = ref<MsgType>({ name: '张三', age: 18 });
const msg: Ref<MsgType> = ref({ name: '张三', age: 18 });
const msg2 = reactive({ name: '张三', age: 18 });

const change = () => {
  // msg.value.name = '李四';
  console.log(msg.value);
  // isRef 判断是否是 ref 响应式数据
  console.log(isRef(msg));
  console.log(isRef(msg2));
}
</script>
    
<style scoped></style>
<template>
  <div>shallowRef {{ msg.name }} {{ msg.age }}</div>
  <hr>
  <div>customRef {{ msg2 }} </div>
  <hr>
  <div ref="dom">我是dom</div>
  <hr>
  <button @click="change">修改</button>
</template>
    
<script setup lang='ts'>
// 导入响应式数据 ref 模块
import { ref, reactive } from 'vue';
// 导入 Ref 类型声明
import { Ref, isRef, shallowRef, triggerRef, customRef } from 'vue';

type MsgType = {
  name: string;
  age: number;
}

// ref 是深层次 shallowRef 是浅层次,ref 和 shallowRef 不能混用
const msg: Ref<MsgType> = shallowRef({ name: '张三', age: 18 });

// ref 获取dom
const dom = ref<HTMLDivElement>();

// customRef 自定义 ref
function myRef<T>(value: T) {
  let timer: any;
  return customRef((track, trigger) => {
    return {
      get() {
        track();
        return value;
      },
      set(newValue) {
        clearTimeout(timer) // 防止抖动,只触发最后一次
        timer = setTimeout(() => {
          console.log('触发了set');
          console.log(dom.value?.innerHTML);

          value = newValue;
          trigger();
        }, 500)
      }
    }
  })
}
const msg2 = myRef<string>('hello');

const change = () => {
  // msg.value.name = '王五'; // 不会触发视图更新
  // msg.value = {
  //   name: '王五',
  //   age: 20
  // };
  // console.log(msg.value);
  msg.value.name = '王五'; // 不会触发视图更新
  triggerRef(msg); // 触发视图更新

  msg2.value = 'world';
}
</script>
    
<style scoped></style>
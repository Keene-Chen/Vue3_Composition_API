<template>
  <!-- 文本插值 -->
  {{ a }}
  <!-- 表达式 -->
  {{ a + 1 }}
  <!-- 三元表达式 -->
  {{ a >= 1 ? '大于1' : '小于1' }}
  <!-- 操作api -->
  {{ b[0].split(',').toString() }}

  <!-- v-text -->
  <div v-text="b"></div>

  <!-- 原始HTML -->
  <div v-html="b[1]"></div>

  <!-- v-if -->
  <div v-if="a >= 1">v-if</div>
  <div v-else-if="a > 2">v-else-if</div>
  <div v-else>v-else</div>

  <!-- v-show -->
  <div v-show="c">v-show</div>

  <!-- 事件绑定 -->
  <button v-on:click="d">点击事件</button>
  <button @click="d">点击事件</button>
  <button @[event]="d">动态事件</button>
  <button @click.middle="d">鼠标中键事件</button>

  <!-- 属性绑定 -->
  <div v-bind:id="f">v-bind属性绑定</div>
  <div :id="f">v-bind简写</div>
  <div :style="g">绑定style</div>
  <div :class="c ? 'true' : 'false'">绑定class</div>
  <div class="f" :class="c ? 'true' : 'false'">支持一个静态class和一个动态class</div>

  <!-- 双向数据绑定 -->
  <div>
    <input type="text" v-model="h" />
    <span>{{ h }}</span>
  </div>

  <!-- v-for -->
  <ul>
    <li v-for="(item, index) in i" :key="index">{{ index }}-{{ item }}</li>
  </ul>

  <!-- v-once -->
  <div v-once>{{ a }}</div>
  <!-- v-memo -->
  <div v-memo>{{ a }}</div>
</template>

<script setup lang="ts">
// 导入响应数据ref
import { ref } from 'vue';

const a: number = 1;
const b: string[] = ['hello,world', '<section>hello,world2</section>'];
const c: boolean = false;
const d = (event: MouseEvent) => {
  console.log('d');
  console.log(event);
}
const event: string = 'dblclick';
const f: string = 'name';
const g = {
  color: 'red',
  border: '1px solid red'
};
const h = ref('hello');
const i: string[] = ['a', 'b', 'c'];
</script>

<style>
#c {
  color: red;
}
</style>

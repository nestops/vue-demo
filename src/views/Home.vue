/* eslint-disable no-undef */
<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App" />
    <a :href="url">href</a>
    <button @click="test($event)">绑定事件</button>
    <p class="nam">表单处理</p>
    <input v-model="message" placeholder="edit me" />
    <input v-model="othermessage" placeholder="edit other me" />
    <input v-model="child" placeholder="child" />
    <div>
      显示标题：getter方法只有当get内部依赖的值发送变化才会执行{{ title }}
    </div>
    <div>
      显示name方法调用：方法调用在html中使用只有有变更检查都会执行{{ name() }}
    </div>
    <div :class="{ active: isActive }">class绑定</div>
    <div v-if="isActive">条件语句v-if</div>

    <ul id="example-1">
      <li v-for="(item, index) in items" :key="item.message">
        {{ item.message }}{{ index }}
      </li>
    </ul>
    <ul id="example-1">
      v-for变量对象
      <li v-for="(value, key, index) in object" :key="key">
        {{ value }}:{{ key }}:{{ index }}
      </li>
    </ul>
    <div>按键事件捕获</div>
    <input v-on:keyup.enter="submit" v-on:keyup.page-down="onPageDown" />
  </div>
</template>
<script lang="ts">
import { Component, Vue, Watch } from 'vue-property-decorator'
import HelloWorld from '@/components/HelloWorld.vue' // @ is an alias to /src

@Component({
  components: {
    HelloWorld
  }
})
export default class Home extends Vue {
  child = '';
  isActive = true;
  _title = '';
  message = '';
  othermessage = '';
  url = 'baidu.com';
  items = [{ message: 'Foo' }, { message: 'Bar' }];
  object = {
    title: 'How to do lists in Vue',
    author: 'Jane Doe',
    publishedAt: '2016-04-10'
  };

  created () {
    console.log('created')
  }

  submit () {
    window.alert('submit')
  }

  test (e: MouseEvent) {
    console.log(e)
    this.isActive = !this.isActive
  }

  name () {
    return new Date()
  }

  onPageDown () {
    window.alert('pagedown')
  }

  get title () {
    return this.message + new Date()
  }

  /**
   * 监听child变量
   */
  @Watch('child')
  onChildChanged (val: string, oldVal: string) {
    console.log(val, oldVal)
  }
}
</script>

<template>
  <div class="left-container">
    <h3>Left 组件</h3>
    <p>msg 的值是：{{ msg }}</p>
    <p>user 的值是：{{ user }}</p>
    <!-- 这个方法可以修改props属性的值但是不能修改父组件 App 中data中的属性值，但是不建议这么使用 -->
    <button @click="msg = 'abc'">修改 msg </button>
    <!-- 使用这个方法可以修改父组件 App 中 data 属性的值，但是不建议这么使用 -->
    <button @click="user.name = 'zs'">修改 user</button>
    <hr>

    <button @click="send">把好诗发给 Right</button>
  </div>
</template>

<script>
// 1. 导入 eventBus.js 模块
import bus from './eventBus.js'

export default {
  props: ['msg', 'user'],
  data() {
    return {
      str: '黑云压城城欲摧，甲光向日金鳞开。'
    }
  },
  methods: {
    send() {
      // 2. 通过 eventBus 来发送数据
      bus.$emit('share', this.str)
    }
  }
}
</script>

<style lang="less">
.left-container {
  padding: 0 20px 20px;
  background-color: orange;
  min-height: 250px;
  flex: 1;
}
</style>

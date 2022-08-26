<template>
  <div class="left-container">
    <h3>Left 组件</h3>
    <p>msg 的值是：{{ msg }}</p>
    <p>user 的值是：{{ user }}</p>
    <!-- 这个方法可以修改props属性的值但是不能修改父组件 App 中data中的属性值，但是不建议这么使用 -->
    <button @click="msg = 'abc'">修改 msg </button>
    <!-- 使用这个方法可以修改父组件 App 中 data 属性的值，但是不建议这么使用 -->
    <button @click="user.name = 'zs'">修改 user</button>
  </div>
</template>

<script>
export default {
  props: ['msg', 'user']
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

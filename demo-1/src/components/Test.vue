<template>
  <div class="test-container">
    <h3>Test.vue 组件</h3>
  </div>
</template>

<script>
export default {
    props: ['info'],
    data() {
        return {
            message: 'hello vue.js'
        }
    },
    methods: {
        show() {
            console.log('调用了 Test 组件的 show 方法！')
        }
    },
    // 创建阶段的第1个什么周期函数
    beforeCreate() {
        console.log(this.info)
        console.log(this.message)
        this.show()
    }
}
</script>

<style lang="less" scoped>
.test-container {
    background-color: pink;
    height: 200px;
}
</style>
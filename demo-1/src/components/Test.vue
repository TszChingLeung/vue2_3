<template>
  <div class="test-container">
    <h3 id="myh3">Test.vue 组件 --- {{ books.length }} 本图书</h3>
    <p id="pppp">message 的值是;{{ message }}</p>
    <button @click="message += '~'">修改 message 的值</button>
  </div>
</template>

<script>
export default {
    props: ['info'],
    data() {
        return {
            message: 'hello vue.js',
            // 定义 books 数组，存储的是所有图书的列表数据。默认为空数组！
            books: []
        }
    },
    methods: {
        show() {
            console.log('调用了 Test 组件的 show 方法！')
        },
        // 使用 Ajax 请求图书列表的数据
        initBookList() {
            const xhr = new XMLHttpRequest()
            xhr.addEventListener('load', () => { // 这里的函数声明 function 会让 this 产生问题，所以要改成箭头函数
                const result = JSON.parse(xhr.responseText)
                console.log(result)
                this.books = result.data
            })

            xhr.open('GET', 'http://www.liulongbin.top:3006/api/getbooks')
            xhr.send()
        }
    },
    // 创建阶段的第1个生命周期函数
    beforeCreate() {
        // console.log(this.info)
        // console.log(this.message)
        // this.show()
    },
    created() {
        // console.log(this.info)
        // console.log(this.message)
        // this.show()

        // created 生命周期函数，非常常用。
        // 经常在它里面，调用 methods 中的方法，请求服务器的数据。
        // 并且，把请求到的数据，转存到 data 中，供 template 模板渲染的时候使用！
        this.initBookList() // 发ajax请求一般建议越早越好，推荐放在 created() 函数中，但是也可以往后挪放到 beforeMount() 中

        // 无法操作DOM因为在 created 方法中组件的模板结构尚未生成(所以这里打印结果为 null)
        // const dom = document.querySelector('#myh3')
        // console.log(dom)
    },
    beforeMount() {
        // console.log('beforeMount')
        // 将要把内存中编译好的 HTML 结构渲染到浏览器中。此时浏览器中还没有当前组件的 DOM 结构，还不能操作DOM（所以打印结果为null）
        // const dom = document.querySelector('#myh3')
        // console.log(dom)
        // console.log(this.$el) // 打印不到 el 元素
    },
    // 如果要操作当前组件的 DOM ，最早，只能在 mounted 阶段执行
    mounted() {
        // console.log(this.$el) // 可以打印到 el 元素
        // const dom = document.querySelector('#myh3')
        // console.log(dom)
    },
    beforeUpdate() {
        // console.log('beforeUpdate')

        // console.log(this.message)
        // const dom = document.querySelector('#pppp')
        // console.log(dom.innerHTML)
    },
    // 当数据变化后，为了能够操作到最新的 DOM 结构，必须把代码写到 updated 生命周期函数中
    updated() {
        // console.log('Updated')

        // console.log(this.message)
        // const dom = document.querySelector('#pppp')
        // console.log(dom.innerHTML)
    },
    beforeDestroy() {
        console.log('beforeDestroy')

        console.log(this.message)
    }
}
</script>

<style lang="less" scoped>
.test-container {
    background-color: pink;
    height: 200px;
}
</style>
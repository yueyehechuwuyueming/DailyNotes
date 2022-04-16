<!-- 本教程学习参考来自@小满zs -->
# 第一章
# 第二章 环境配置
[vite配置教程](https://blog.csdn.net/qq1195566313/article/details/122769982)
注：用pnpm代替npm
# 第三章 Vite目录 & Vue单文件组件
- vite目录
    - public 存放无需被编译的静态资源，如图片，js文件
    - src
        - assert 存放可编译的静态资源，如打包过程中把4kb图片导报成base64格式
        - conponents 存放公共组件，如页头页尾（很多地方都需要用）
        - App.vue 全局组件
        - main.ts 全局的ts文件，公共的api？可放入
    - index.html 非常重要的入口文件
        -  webpack，rollup 他们的入口文件都是entry
        - input 是一个js文件 而Vite 的入口文件是一个html文件，他刚开始不会编译这些js文件 只有当你用到的时候 如script src="xxxxx.js" 会发起一个请求被vite拦截这时候才会解析js文件
    - package.json 配置文件，命令、依赖包等
    - tsconfig.json TS的配置文件
    - vite.config.ts vite的配置文件具体配置项 
- SFC(Single File Conponent)语法规范
    - vue件都由三种类型的顶层语法块所组成<template>、<script>、<style>
    - <template> 放标签 只能写一个
        - 每个 *.vue 文件最多可同时包含一个顶层 <template> 块
        - 其中的内容会被提取出来并传递给 @vue/compiler-dom，预编译为 JavaScript 的渲染函数，并附属到导出的组件上作为其 render 选项。？
    - <script> 写js逻辑 可写多个
        - 每一个 *.vue 文件最多可同时包含一个 <script> 块 (不包括<script setup>)。
        - 该脚本将作为 ES Module 来执行
        - 其默认导出的内容应该是 Vue 组件选项对象，它要么是一个普通的对象，要么是 defineComponent 的返回值
        - <script setup> 只能写一个
    - <style> 放样式，可写多个
        - 一个 *.vue 文件可以包含多个 <style> 标签
        - <style> 标签可以通过 scoped 或 module attribute (更多详情请查看 SFC 样式特性) 将样式封装在当前组件内。多个不同封装模式的 <style> 标签可以在同一个组件中混用
- 指令(v开头都是vue指令)
    - v-text:显示文本
    - v-html:显示富文本(里面可写html语句)
    - v-if:隐藏/显示 false/true(把整个结点注释掉，浪费性能，性能差)
    ![20220410084100](https://s2.loli.net/2022/04/10/LCRNAjQrHMtnp4W.png)
    - v-show:隐藏/显示 false/true(只操作css，display none切换，性能好)
    ![20220410083850](https://s2.loli.net/2022/04/10/OQYkIwXsidRmFz5.png)
    - v-if/v-else-if/v-else：条件语句
    ```html
    <div>
        <div v-if="flag1 == 'A'">A</div>
        <div v-else-if="flag1 == 'B'">B</div>
        <div v-else-if="flag1 == 'C'">C</div>
        <div v-else>D</div>
    </div>
    ```
    - v-on:可简写@(v-on:=@),用来给元素添加事件
    ![20220410085735](https://s2.loli.net/2022/04/10/hvAwF4NQufUI5Cm.png)
    ![20220410221105](https://s2.loli.net/2022/04/10/QxV8JENujgcstMm.png)
    ![20220410221442](https://s2.loli.net/2022/04/10/YjRIo5y2safnieN.png)
    - 阻止表单提交(阻止界面刷新)
    ```TS
        <template>
            <form action="/">
                <button @click.prevent="submit" type="submit">submit</button>
            </form>
        </template>
        
        <script setup lang="ts">
        const submit = () => {
        console.log('child');
        
        }      
        </script>
    ```
    - v-bind:用来绑定元素的属性Attr
    ```TS
    //方法一
    <script setup lang="ts">
    type Style = {
        color:string,
        height:string
    }
    const style1:Style = {
        color:"blue",
        height:"2000px"
    }
    </script>

    <template>
        <div v-bind:style="style1">
        我是233
        </div>
    </template>

    //方法二
    
    ```
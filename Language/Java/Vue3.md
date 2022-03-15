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
    - index.html 
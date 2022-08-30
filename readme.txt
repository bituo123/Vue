Vue的学习
主要从双向绑定，Template，动态Class，Style，组件，router开始学习
最后用一个实战进行收尾
Vue的工程目录
assets主要存放资源文件，css，js，images，
componets存放vue开发中一些组件，如header.vue,footer.vue等
router路由配置文件
views页面文件
app.vue根组件
main.js项目的入口文件，定义了vue实例，引入了根组件app.vue并把他挂载到index中id为app的节点上
在vue里面，template对应HTMl，script对应JS，style对应CSS
template中只能有一个块标签，其他所有的标签都必须在块里面
vue的声明式渲染，在template使用<h2>{{title}}</h2>，在script里面定义
<script>
  export default {
    // 模块的名字
    name: "app",
    // 页面中数据存放的地方
    data() {
      return {
        title: "优课达--学的比别人好一点"
      };
    }
  };
</script>
双向绑定-用户输入的数据绑定到变量中，从而可以在别的地方引用
在输入的标签中加上v-model="message"属性，在script的数据中加上message: ""，就可以在其他地方用{{}}引用

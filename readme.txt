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
vue绑定事件v-on:click=""或者@click
方法写在script里
methods:{
        alertFn:function(){
            alert("Hello World");
        }
    }
阻止冒泡事件
@click.stop="fn2"
捕获事件
@click.capture="fn2"
阻止默认事件
@click.prevent="fn2"
监听数据变化
watch: {
      count() {
        console.log("count发生了变化");
      }
watch里面的变量名一定要和data里面的变量名一样
方法加两个参数，value，oldvalue分别表示新值和旧值
监听器还包换一个handler和immediate属性
如果immediate的值为immediate: true不论数据是否变化，页面刷新以后handler方法就会执行
绑定标签属性值
v-bind:alt="imgText"可以省略为:alt
模板表达式{{ goods[0].index + 1 }}
三元表达式{{ flag?'你已经通过了考试':'你还没有通过考试' }}
模板写方法{{ message.split('').reverse().join('') }}
条件渲染
<p v-if="isShow">{{ message }}</p>
<p v-else>{{ defaultMessage }}</p>
方法返回的是boolean
多条件
<p v-if="questions[0].type==='PICK'">{{ questions[0].content }}</p>
<p v-else-if="questions[1].type==='MULT'">{{ questions[1].content }}</p>
<p v-else>题目还没有加载进来...</p>
v-show指令也是满足条件显示，但是v-show是display显示为none，v-if指令是在dom直接不存在
循环使用
<ul>
    <li v-for="item in 5" :key="item">{{ item }}</li>
</ul>
这是遍历5
<ul>
    <li v-for="(item,index) in nameList" :key="index">{{ item }}</li>
</ul>
这是遍历数组
可以加序号{{ index }}---{{ item }}
可以加表达式
{{ index+1 }}
for的三个参数
value：对象中每一项的值
key：对象中每一项的键
index：索引
计算属性computed
与方法的区别是，计算属性的对象如果发生变化，计算会重新计算，返回结果，不发生变化会返回缓存的值不计算
方法是每次访问的时候都会去执行方法体的逻辑
动态样式绑定
v-bind:class="{ active: isActive }"如果说类名是有字符，则需要加上双引号单引号'base-active': isActive
多类名写法"base-active": isActive,"base":true
其中的boolean在data里面
data:function(){
    return {
        isActive:false
    }
}
最后通过事件来改变布尔值，从而改变动态绑定的样式

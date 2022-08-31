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
动态style
<div :style="flexStyle"></div>
data:function(){
    return {
        flexStyle: {
            display: 'flex',
            flexDirection: 'column',
            justifyContent: 'space-between',
            alignItems: 'center',
            flexWrap: 'no-wrap',
        },
    }
}
但是如果像动态壁纸这样就不能用data里面写css，需要div里面写url(${imgUrls[currentIndex]})引用
因为写在data里面的不能引用，不过可以试试this行不行
自定义组件
组件的注册，全局注册和局部注册两种，
Vue.component创建全局注册，注册后在任何新创建的Vue根实例中使用
局部注册，在单个Vue格式的文件中创建组件，在需要用到的地方进行注册
一般在component目录里创建vue文件，在data里面加上name作为组件名称
在另一个文件里使用组件，<HelloWorld></HelloWorld>
在script里面导入import HelloWorld from 文件路径
在script里面注册组件components:{HelloWorld}
自定义组件中的数据必须是一个函数，相互独立的
组件单向数据流
prop使用方法，
:title="title1"注意tittle1是父组件的data变量，tittle是子组件定义的变量
子组件
<h1>{{ title }}</h1>
data中加上props: ['title']
props: {
      title: String
    }
props: {
  title: String,
  // 多类型
  likes: [String, Number],
  // 带有默认值
  isPublished: {
    type: Boolean,
    default: true
  },
  // 必填
  commentIds: {
    type: Array,
    required: true
  },
  author: Object,
  callback: Function,
  contactsPromise: Promise
}
子组件处理父组件传入的信息
props: ['initialTitle'],
computed: {
  normalizedTitle: function () {
    // 对传入的 initialTitle 进行去空格、字母小写化处理
    return this.initialTitle.trim().toLowerCase()
  }
}
自定义组件绑定原生事件
在自定义组件的根元素上监听一个原生组件和在html原生标签上监听一个原生事件是有区别的
父组件和子组件的绑定，父组件和子组件同时加上事件，最后只有子组件发生
为了让父组件也发生需要给父组件加上@click.native="print(article)"
按键修饰符
@keyup.enter="print(article)"
给子组件绑定自定义事件
父组件在调用子组件的时候加上v-on:upVote="handleLikes"
upVote是事件名称
<button @click="$emit('upVote')">点赞</button>是子组件调用
如果还需要加别的功能，可以这样写
<button @click="childEvent">点赞</button>
methods: {
  childEvent: function() {
    // 调用自定义事件 upVote
    this.$emit('upVote');
    // do other things
  }
}

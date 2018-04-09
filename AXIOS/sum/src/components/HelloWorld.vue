<template>
  <div class="hello">
    <h3>{{ msg }}</h3>
    <p>
      1、 安装npm install --save axios <br>
      2、进main.js引入 axios <br>
      3、先进入config文件夹当中的index.js配置 <br>
      4、然后进入main.js配置Vue.prototype.HOST = "/api" <br>
      注意：配置完成要重启npm run dev

    </p>
    <!-- 遍历数据 -->
    <ul v-for="text in tet">
      <li>
          {{ text.title }} <br>
          <img :src="text.img" alt="">
      </li>

    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'axios跨域测试',
      tet:[] // 空数组接收数据
    }
  },
  created(){
    //  api接口 "https://api.douban.com/v2/movie/in_theaters"
    let url = this.HOST + "/movie/in_theaters";
    this.$axios.get(url,{
      params:{
        count:15, // count代表获取多少条数据
        start:0  // start代表从0开始获取
      }
    })
    .then(res=>{
      console.log(res)
      this.fen(res.data) // 传数据给下面的函数方法
    })
    .catch(error=>{
      console.log(error)
    })
  },
  // 过滤数据
  methods:{
    fen(data){
      var arr = []; // 设置一个空数组
      // 遍历里面的数据
      for(var i=0;i<data.subjects.length;i++){
        var mov = {
          title : data.subjects[i].title,
          img : data.subjects[i].images.large
        }
        arr.push(mov); // 吧遍历过后的数据给空数组添加
      }
      this.tet = arr; // 添加后的数组赋值给data定义好的空数组
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

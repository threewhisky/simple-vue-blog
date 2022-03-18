<template>
  <div id="show-blogs" v-theme:column="'narrow'">
    <h1>博客总览</h1>
    <div class="search">
      <input type="text">
    </div>

    <div class="bloglist">
      <div class="single-blog" v-for="blog in blogs" v-bind:key="blog.id">
        <h2 v-rainbow>{{blog.title}}</h2>
        <article>{{blog.body}}</article>

      </div>
    </div>

  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'show-blogs',
  data () {
    return {
      blogs: [],
    }
  },
  // 自定义指令注册和使用
  directives: {
    rainbow: function (el, binding) {
      // 随机彩虹色显示博客标题
      el.style.color = '#' + Math.random().toString(16).slice(2,8);
    },
    theme: function(el, binding) {
      //拿到自定义指令的值
      if (binding.value == 'wide') {
        el.style.maxWidth = '1200px';
      }else if (binding.value == 'narrow') {
        el.style.maxWidth = '500px';
      }
      // 拿到自定义指令的参数
      else if (bingding.arg == 'column') {
        el.style.background = '#6677cc';
        el.style.padding = '20px';
      }
    },
  },
  created () {
    // 请求数据
    axios.get('https://jsonplaceholder.typicode.com/posts')
      .then((data) => {
        this.blogs = data.data.slice(0,10);
      });
  },

}
</script>

<style>
#show-blogs {
  max-width: 600px;
  margin: 0 auto;
}

.single-blog {
  padding:20px;
  margin: 20px 0;
  box-sizing: border-box;
  background-color: #eee;
}

</style>

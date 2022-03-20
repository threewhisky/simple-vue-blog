<template>
  <div id="show-blogs" v-theme:column="'wide'">
    <h1>博客总览</h1>
    <div class="search">
      <input type="text" placeholder="搜索" v-model="search">
    </div>

    <div class="bloglist">
      
      <div class="single-blog" v-for="blog in searchBlogs" v-bind:key="blog.id">
        <router-link :to='"/blog/" + blog.id'>
          <h2 v-rainbow>{{ toUpper(blog.title) }}</h2>
          <article>{{ snippet(blog.body) }}</article>
        </router-link>
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
      search: '',
    }
  },

  created () {
    // 请求数据
    axios.get('https://jsonplaceholder.typicode.com/posts')
      .then((data) => {
        this.blogs = data.data.slice(0,10);
      });
  },
  computed: {
    toUpper() {
      // 把标题全部大写
      return (title) => {
        return title.toUpperCase();
      }
    },
    snippet () {
      // 给博客内容打点
      return (body) => {
        return body.slice(0,100) + '...';
      }
    },
    searchBlogs() {
      // 筛选搜索出的博客

      return this.blogs.filter((blog) => {
        return blog.title.match(this.search); // 这里只是返回true或者false
      });
    },
  },
  // 自定义指令注册和使用
  directives: {
    // 想自定义指令只生效一次，就用bind来写
    rainbow: {
      bind(el) {
        // 随机彩虹色显示博客标题
        el.style.color = '#' + Math.random().toString(16).slice(2,8);
      },
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

}
</script>

<style scoped>
h1{
  text-align: center;
}
input{
  display: block;
  width:80%;
  margin: 0 auto;
  padding: 8px;
}
#show-blogs {
  max-width: 600px;
  margin: 0 auto;
}

.single-blog {
  padding:20px;
  margin: 20px 0;
  box-sizing: border-box;
  background-color: #eee;
  border: 1px dotted #aaa;
}

#show-blogs a{
  color: #444;
  text-decoration: none;
}



</style>

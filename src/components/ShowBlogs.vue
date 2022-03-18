<template>
  <div id="show-blogs">
    <h1>博客总览</h1>
    <div class="search">
      <input type="text">
    </div>

    <div class="bloglist">
      <div class="single-blog" v-for="blog in blogs" v-bind:key="blog.id">
        <h2>{{blog.title}}</h2>
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
  created () {
    // 请求数据
    axios.get('https://jsonplaceholder.typicode.com/posts')
      .then((data) => {
        // console.log(data.data);
        this.blogs = data.data.slice(0,10);
        // console.log(this.blogs);
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

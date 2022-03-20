<template>
  <div id="app">
    <!-- <add-blog></add-blog> -->
    <!-- <show-blogs></show-blogs> -->
    <blog-header></blog-header>
    <router-view></router-view>
    <!-- <router-link to="/">Home</router-link>
    <router-link to="/add">About</router-link>   -->
  </div>
</template>

<script>
import AddBlog from './components/AddBlog.vue'
import ShowBlogs from './components/ShowBlogs.vue'
import BlogHeader from './components/BlogHeader.vue'


export default {
  name: 'app',
  components: {
    'add-blog': AddBlog,
    'show-blogs':ShowBlogs,
    'blog-header': BlogHeader,
  }
}
</script>

<style>

</style>

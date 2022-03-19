<template>
  <div id="app">
    <!-- <add-blog></add-blog> -->
    <show-blogs></show-blogs>
  </div>
</template>

<script>
import AddBlog from './components/AddBlog.vue'
import ShowBlogs from './components/ShowBlogs.vue'

export default {
  name: 'app',
  components: {
    'add-blog': AddBlog,
    'show-blogs':ShowBlogs,
  }
}
</script>

<style>

</style>

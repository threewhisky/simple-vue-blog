<template>
  <div class="add-blog">
    <h1>添加博客</h1>
    <form>
      <label>博客标题：</label>
      <input type="text" v-model="blog.title" required/>
      <br/>

      <label>博客内容：</label>
      <textarea v-model="blog.content"></textarea>
      <br/>

      <p>博客分类：</p>
      <div id="checkboxes">
        <label for="Vue.js">Vue.js</label>
        <input type="checkbox" id="Vue.js" value="Vue.js" v-model="blog.categories">
        <label for="React.js">React.js</label>
        <input type="checkbox" id="React.js" value="React.js" v-model="blog.categories">
        <label for="Angular.js">Angular.js</label>
        <input type="checkbox" id="Angular.js" value="Angular.js" v-model="blog.categories">
        <label for="Node.js">Node.js</label>
        <input type="checkbox" id="Node.js" value="Node.js" v-model="blog.categories">
      </div>

      <p>博客作者：</p>
      <select v-model="blog.author">
        <option v-for="author in authors" v-bind:key='author'>{{author}}</option>
      </select>

    </form>

    <hr/>

    <div class="preview">
      <h2>博客总览</h2>
      <p>博客标题：{{blog.title}}</p>
      <p>博客内容：{{blog.content}}</p>
      <p>分类：</p>
        <ul>
          <li v-for="category in blog.categories" v-bind:key="category">
            {{category}}
          </li>
        </ul>
      <p>作者：{{blog.author}}</p>
    </div>

  </div>
</template>

<script>
export default {
  name: 'add-blog',
  data () {
    return {
      blog: {
        title: '',
        content: '',
        categories:[],
        author: '',
      },
      authors: ['Mark','Max','Bob'],
    }
  },
}
</script>

<style scoped>

</style>

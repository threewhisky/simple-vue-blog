<template>
  <div id="add-blog">
    <h1>添加博客</h1>
    <form v-if="!submitted">
      <label>博客标题：</label>
      <input type="text" v-model="blog.title" required/>

      <label>博客内容：</label>
      <textarea v-model="blog.content"></textarea>

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

      <button @click.prevent="post">添加博客</button>

    </form>

      <h3 v-if="submitted">您的博客发布成功</h3>

    <div id="preview">
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
import axios from 'axios'
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
      submitted: false,
    }
  },
  methods: {
    post: function() {
      // https://jsonplaceholder.typicode.com/posts
      axios.post('https://jsonplaceholder.typicode.com', {
        title: this.blog.title,
        content: this.blog.content,
      })
        .then((data) => {
          this.submitted = true;
        })
    }
  }
}
</script>

<style scoped>
#add-blog *{
  box-sizing: border-box;
}

#add-blog {
  margin: 20px auto;
  max-width: 600px;
  padding: 20px;
}

textarea {
  height: 200px;
}

p {
  padding: 0;
  margin: 20px 0 0;
}

input[type="text"],textarea,select{
  display: block;
  width:100%;
  margin:0 0 8px;
} 

input[type="checkbox"]{
  margin: 0 20px 0 0;
}

button {
  display: block;
  background: crimson;
  color: #fff;
  border: 0;
  padding: 14px;
  border-radius: 4px;
  font-size: 18px;
  cursor: pointer;
}

#preview{
  padding:10px 20px;
  border: 1px dotted #ccc;
  margin:30px 0;
}
</style>

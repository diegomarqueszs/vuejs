<template>
    <div class="container">
    <h1>Comentários</h1>
    <hr />
    <formTodo v-on:add-todo="addComment"></formTodo>
    <div class="list-group">
      <p v-if="comments.length<=0">Sem comentários...</p>
      <div class="list-group-item" v-for="(comment, index) in allComments" :key="index">
        <span class="comment_author">Autor: <strong>{{ comment.name }}</strong></span>
        <p>{{ comment.message }}</p>
        <div>
        <a href="#" title="Excluir" v-on:click.prevent="removeComment(index)">Excluir</a>
      </div>
      </div>
    </div>
    <hr />
  </div>
</template>

<script> 
import formTodo from './form-todo'

export default{
  name: 'CommentsList',
  components: {
    formTodo
  },
    data(){
    return{
        comments: [],
    }
  },
  methods:{
    addComment(comment){
      this.comments.push(comment);
    },
    
    removeComment(index){
        this.comments.splice(index, 1); 
    },
  },
  computed: {
    allComments(){
        return this.comments.map(comment =>({
            ...comment,
            name: comment.name.trim() === '' ? 'Anônimo' : comment.name
        }))
    }
  },
  watch: {
    comments(val) {
        console.log('val',val)
    }
  }
}
</script>


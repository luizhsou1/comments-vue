<template>
  <div class="container">
    <h1>Comentários</h1>
    <hr />
    <commentForm v-on:add-comment="addComment" />
    <br />
    <p v-if="!comments.length">Sem Comentários...</p>
    <div class="list-group">
      <div
        class="list-group-item"
        v-for="(comment, index) in allComments"
        v-bind:key="index"
      >
        <span class="comment_author">
          Autor: <strong>{{ comment.name }}</strong>
        </span>
        <p>{{ comment.message }}</p>
        <div>
          <a v-on:click.prevent="removeComment(index)" href="#" title="Excluir"
            >Excluir</a
          >
        </div>
      </div>
    </div>
    <hr />
  </div>
</template>

<script>
import CommentForm from "./CommentForm.vue";

export default {
  components: {
    CommentForm,
  },
  data() {
    return {
      comments: [],
    };
  },
  methods: {
    addComment(comment) {
      this.comments.push(comment);
    },
    removeComment(index) {
      this.comments.splice(index, 1);
    },
  },
  computed: {
    allComments() {
      return this.comments.map((comment) => ({
        ...comment,
        name: comment.name.trim() === "" ? "Anônimo" : comment.name,
      }));
    },
  },
  watch: {
    // Monitora a propriedade comments, qualquer mudança no array de comments, ele chama essa função
    comments(val) {
      console.log(val);
    },
  },
};
</script>

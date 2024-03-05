<template>
  <div class="main">
    <div class="booksContainer">
      <h3>Cards go here</h3>
      <div
        class="cardContainer"
        v-for="(book, index) in books"
        :key="index"
        draggable="true"
        @dragstart="handleDragStart(book.id)"
      >
        <b-card
          :title="book.name"
          tag="article"
          style="max-width: 20rem"
          class="mb-2"
        >
          <img :src="book.urlImage" class="card-img-top" alt="..." />
          <b-card-text>Nombre : {{ book.name }} </b-card-text>
          <b-card-text>Autor: {{ book.author }} </b-card-text>
          <b-card-text
            >Fecha de publicación: {{ book.publishDate }}</b-card-text
          >
        </b-card>
      </div>
      <div class="optionsContainer">
        <div
          class="updateContainer"
          @dragover.prevent
          @drop="handleDrop('edit')"
        >
          <h3>Editar</h3>
        </div>

        <div
          class="deleteContainer"
          @dragover.prevent
          @drop="handleDrop('delete')"
        >
          <h3>Eliminar</h3>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Vue from "vue";
export default Vue.extend({
  data() {
    return {
      books: [],
      draggedBookId: null,
    };
  },
  methods: {
    handleDragStart(bookId) {
      this.draggedBookId = bookId;
    },
    handleDrop(action) {
      if (action === "edit") {
        console.log("Editando libro con ID:", this.draggedBookId);
      } else if (action === "delete") {
        console.log("Eliminando libro con ID:", this.draggedBookId);
      }
    },
  },
});
</script>

<style>
.main {
  display: flex;
}
.booksContainer {
  display: flex;
  flex-wrap: wrap;
  padding: 0% 1% 1% 1%;
  justify-content: space-between;
}
.cardContainer {
  padding: 1%;
}
.optionsContainer {
  width: 300px;
}
.updateContainer {
  background-color: rgb(255, 180, 19);
  height: 100px;

  display: flex;
  justify-content: center;
  align-items: center;
}
.deleteContainer {
  background-color: #ff0000;
  height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.optionsContainer div {
  margin-top: 10px;
  text-align: center;
  padding: 5px;
  border: 1px solid #ccc;
}
.optionsContainer div:hover {
  background-color: #f0f0f0;
  cursor: pointer;
}
</style>

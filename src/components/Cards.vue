<template>
<div class="main">
        <div class="booksContainer">
            <h3>Cards go here</h3>
            <div class="cardContainer"
            v-for="(book, index) in books"
            :key="index">
            
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
              >Fecha de publicación: {{ book.publishDate }}
            </b-card-text>
          </b-card>
            </div>
        </div>


    <div class="optionsContainer">
        <div class="updateContainer"> <h3>Editar</h3></div>
           
        <div class="deleteContainer"><h3>Eliminar</h3></div>
            
        </div>
</div>
</template>

<script>
import Vue from 'vue';
export default Vue.extend({
    data(){
        return{
            books: []
        }
    }
})
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
    height: 50%;
}
.updateContainer{
    background-color: rgb(255, 180, 19);
}
.deleteContainer{
    background-color: #ff0000;
}
</style>
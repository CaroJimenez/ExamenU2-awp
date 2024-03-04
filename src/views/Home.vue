<template>
    <div class="main">
        <div class="filtersContainer"></div>
                <h1>Filtros</h1>
                <AddBook/>
            
            <Cards/> 
    </div>

</template>

<script>
import Vue from "vue";
import AddBook from "../components/AddBook.vue"
import Cards from "../components/Cards.vue";
export default Vue.extend({
    components:{
    AddBook,
    Cards
    }
})
</script>

<style>
.main {
  display: flex;
}
.bodyConatiner{
}
.filtersContainer{
    flex-direction: column;
}
</style>
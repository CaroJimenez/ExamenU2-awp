<template>
  <div>
    <b-button variant="primary" @click="openModal">Nuevo libro</b-button>

    <b-modal v-model="showModal" title="Nuevo libro" hide-footer>
      <b-form @submit.prevent="submitForm">
        <b-form-group
          id="bookName"
          label="Nombre del libro"
          label-for="bookName"
          :state="!errors.bookName ? true : false"
          :invalid-feedback="errors.bookName"
        >
          <b-form-input
            id="bookName"
            v-model="bookName"
            type="text"
            placeholder="Nombre del libro"
            required
          ></b-form-input>
        </b-form-group>
        <b-form-group
          id="author"
          label="Autor"
          label-for="author"
          :state="!errors.author ? true : false"
          :invalid-feedback="errors.author"
        >
          <b-form-input
            id="author"
            v-model="author"
            type="text"
            placeholder="Autor del libro"
            required
          ></b-form-input>
        </b-form-group>
        <!--Fecha de publicación-->
        <b-form-group
          id="publishDate"
          label="Fecha de publicación"
          label-for="publishDate"
          :state="!errors.publishDate ? true : false"
          :invalid-feedback="errors.publishDate"
        >
          <b-form-input
            id="publishDate"
            v-model="publishDate"
            type="text"
            placeholder="Fecha de publicación de la película"
            required
          ></b-form-input>
        </b-form-group>
        <!--Imagen-->
        <b-form-group id="file" label-for="file">
          <b-form-file
            v-model="file"
            :state="Boolean(file)"
            placeholder="Selecciona una imagen"
          ></b-form-file>
        </b-form-group>
        <b-button type="submit" variant="primary">Registrar</b-button>
      </b-form>
    </b-modal>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      showModal: false,
      bookName: "",
      author: "",
      publishDate: "",
      file: null,
      errors: {},
    };
  },
  methods: {
    openModal() {
      this.showModal = true;
    },
    async submitForm() {
      this.errors = {};
      if (!/^[a-zA-Z\s\W]+$/.test(this.bookName)) {
        this.errors.bookName = "El nombre del libro no puede estar vacío";
      }
      if (!/^[a-zA-Z\s\W]+$/.test(this.author)) {
        this.errors.author = "El autor no puede quedar vacío";
      }
      if (!/^\d{4}-\d{2}-\d{2}$/.test(this.publishDate)) {
        this.errors.publishDate =
          "El formato de la fecha no es correcto, debe ser YYYY-MM-DD";
      }
      const formData = {
        name: this.bookName,
        author: this.author,
        publishDate: this.publishDate,
      };
      this.agregarLibro(formData);
    },
    async agregarLibro(formData) {
      try {
        const fd = new FormData();
        fd.append(
          "bookRequestDTO",
          new Blob([JSON.stringify(formData)], { type: "application/json" })
        );
        const response = await axios.post(
          "http://localhost:8080/books/add",
          fd
        );

        console.log("Respuesta del servidor:", response.data);
      } finally {
        this.showModal = false;
        location.reload();
      }
    },
  },
};
</script>

<style></style>

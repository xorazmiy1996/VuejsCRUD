<template>
  <div class="move-add-form">
    <h3>Yangi kino qo'shish</h3>
    <form class="add-form d-flex" action="">
      <input type="text" class="form-control new-movie-label" placeholder="Qanday kino?"
             :value="name"
             @input="name=$event.target.value"
      />
      <input type="number" class="form-control new-movie-label" placeholder="Necha marotaba ko'rilgan?"
             :value="viwers"
             @input="viwers=$event.target.value"
      />
      <button @click="addMovie" class="btn btn-outline-dark" type="submit">Qo'shish</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "MoveAddForm",
  data() {
    return {
      name: "",
      viwers: "",
    }
  },

  methods: {
    addMovie(e) {
      e.preventDefault()
      if (!this.name || !this.viwers) return
      const newMovie = {
        name: this.name,
        viewers: this.viwers,
        favorite: false,
        like: false,
        id:Date.now(),
      }
      this.$emit("createMovie",newMovie);
      this.name='';
      this.viwers='';
    }

  },


}
</script>

<style scoped>
.move-add-form {
  margin-top: 2rem;
  padding: 1.5rem;
  border-radius: 4px;
  box-shadow: 15px 15px 15px rgba(0, 0, 0, 0.15);
  background-color: #fcfaf5;
}
</style>
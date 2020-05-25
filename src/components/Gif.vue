<template>
  <div class="gif">
    <h4>{{ msg }}</h4>
    <form @submit.prevent="search">
      <input type="text" placeholder="Título" v-model="cat.title" />

      <label>Filtro:</label>
      <select name="filtro" @change="filterChange($event)">
        <option value="blur">Blur</option>
        <option value="mono">Mono</option>
        <option value="sepia">Sepia</option>
        <option value="negative">Negative</option>
        <option value="paint">Paint</option>
        <option value="pixel">Pixel</option>
      </select>

      <label>Color:</label>
      <select name="color" @change="colorChange($event)">
        <option value="green">Verde</option>
        <option value="blue">Azul</option>
        <option value="yellow">Amarillo</option>
        <option value="red">Rojo</option>
        <option value="pink">Rosado</option>
        <option value="white">Blanco</option>
        <option value="black">Negro</option>
      </select>

      <input v-model="cat.size" type="number" placeholder="Tamaño" />

      <button @click="search">
        <i id="manito" class="fas fa-paw"></i>
      </button>
    </form>

    <span v-show="cat.isLoading">Buscando gato...</span>
    <img v-show="!cat.isLoading" :src="cat.src" alt />
  </div>
</template>

<script>
export default {
  name: "Gif",
  props: {
    msg: String
  },
  data() {
    return {
      cat: {
        src: "",
        title: "",
        filter: "",
        color: "",
        size: "",
        isLoading: false
      }
    };
  },
  methods: {
    search() {
      this.cat.isLoading = true;
      fetch(
        `https://cataas.com/cat/gif/says/${this.cat.title}?filter=${this.cat.filter}&color=${this.cat.color}&size=${this.cat.size}`
      )
        .then(response => (this.cat.src = response.url))
        .then(() => (this.cat.isLoading = false));
    },
    filterChange(event) {
      this.cat.filter = event.target.value;
    },
    colorChange(event) {
      this.cat.color = event.target.value;
    }
  },
  computed: {
    title() {
      return this.cat.title;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.gif {
  width: 60%;
  background-color: pink;
  margin: auto;
  border-radius: 15px;
}

form {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-content: center;
  flex-wrap: wrap;
  padding: 30px;
}

button {
  background-color: #d10069;
  color: white;
  border-radius: 10px;
  border: 0;
  width: fit-content;
  align-self: center;
  margin-top: 30px;
}
#manito {
  padding: 20px;
  font-size: 50px;
}

input {
  margin: 10px;
  width: 250px;
  padding: 10px;
  font-size: 20px;
  border: 0;
  border-radius: 5px;
}

select {
  margin: 10px;
  margin-top: 0px;
  padding: 10px;
  font-size: 20px;
  font-weight: 500;
  border: 0;
  border-radius: 5px;
  color: grey;
}
</style>

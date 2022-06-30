<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <p>
      <label for="elTitulo">Titulo:</label> <input name="elTitulo" id="elTitulo"
        type="text" v-model="titulo">
    </p>

    <p>
    <label for="elFiltro">Filtro:</label>
    <select v-model="filtro" name="elFiltro" id="elFiltro">
      <option value="blur">Blur</option>
      <option value="mono">Mono</option>
      <option value="sepia">Sepia</option>
      <option value="negative">Negative</option>
      <option value="paint">Paint</option>
      <option value="pixel">Pixel</option>
    </select>
    </p>

    <p>
    <label for="elColor">Color:</label>
    <select v-model="color" name="elColor" id="elColor">
      <option value="green">Verde</option>
      <option value="yellow">Amarillo</option>
      <option value="blue">Azul</option>
      <option value="red">Rojo</option>
      <option value="orange">Naranja</option>
      <option value="pink">Rosa</option>
    </select>
    </p>

    <p>
      <label for="elTamano">Tamaño:</label> <input name="elTamano" id="elTamano"
        type="number" v-model="tamano">
    </p>

    <button v-on:click="buscargato">obtener mi gatito</button></p>

    <DatosGato v-bind:laImagen = "urlimagen" msg="Datos del Gatito"/>
  </div>
</template>

<script>
import DatosGato from './components/DatosGato.vue'

export default {
  name: 'App',
  components: {
    DatosGato
  },
  data(){
    return{
        titulo: '',
        filtro:'',
        color: '',
        tamano: '',
        urlimagen:'',
    }
  },
  methods: {
        buscargato(){
        this.limpiar();

        // let url = `https://cataas.com/cat/gif/says/${this.titulo}?filter=${this.filtro}&color=${this.color}&size=${this.tamano}&type=or`;
           let url = 'https://cataas.com/cat/gif/says/'+this.titulo+'?filter='+this.filtro+'&color='+this.color+'&size='+this.tamano+'&type=or';


        console.log('url armada: ');
        console.log(url);
        fetch(url)
        .then(response => {
                console.log(response);
                this.urlimagen = response.url;

                });

      },
      limpiar(){
        console.log('se invoca limpiar');

      }, //fin limpiar

  },
  created(){
      this.buscargato();
}, //fin created
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

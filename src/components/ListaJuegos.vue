<script>
import { useJuegosStore } from '@/stores/juegos'
import { mapStores } from 'pinia'

export default {
  name: 'ListaJuegos',
  computed: {
    ...mapStores(useJuegosStore)
  },
  created() {
    this.juegosStore.fetchJuegos()
  },
  mounted() {
    console.log(this.juegosStore)
  },
  methods: {
    aumentarStock(codigo) {
      this.juegosStore.agregarStock(codigo)
    },
    disminuirStock(codigo) {
      this.juegosStore.quitarStock(codigo)
    }
  }
}
</script>

<template>
  <div>
    <h2 class="text-center">Lista de Juegos</h2>
    <table>
      <thead>
        <tr>
          <th>Código</th>
          <th>Nombre</th>
          <th>Stock</th>
          <th>Precio</th>
          <th>Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="juego in juegosStore.juegos" :key="juego.codigo">
          <td>{{ juego.codigo }}</td>
          <td>{{ juego.nombre }}</td>
          <td>{{ juego.stock }}</td>
          <td>{{ juego.precio }}</td>
          <td>
            <button @click="aumentarStock(juego.codigo)">Agregar</button>
            <button class="mleft" @click="disminuirStock(juego.codigo)">Quitar</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
}

th,
td {
  border: 1px solid #ddd;
  padding: 8px;
  text-align: center;
}

th {
  background-color: #f2f2f2;
}

.text-center {
  text-align: center;
}

.mleft {
  margin-left: 1rem;
}
</style>

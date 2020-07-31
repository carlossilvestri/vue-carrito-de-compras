<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-md-7">
          <div class="row">
            <div class="col-md-6" v-for="i in productos" :key="i.id">
              <producto
                :producto="i"
                v-on:agregar-carro="agregarCarro"
                :estaEnCarrito="estaEnCarrito(i)"
              />
            </div>
          </div>
        </div>
        <div class="col-md-5 my-5">
          <carrito :items="carrito" v-on:remover-item="removerProducto" v-on:pagar="pagar" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import productos from "./productos.json";
import Producto from "./components/Producto.vue";
import Carrito from "./components/Carrito.vue";

export default {
  name: "App",
  components: {
    Producto,
    Carrito,
  },
  data() {
    return {
      productos,
      carrito: [],
    };
  },
  methods: {
    agregarCarro(producto) {
      this.carrito.push(producto);
    },
    estaEnCarrito(producto) {
      const item = this.carrito.find((item) => item.id === producto.id);
      if (item) {
        return true;
      } else {
        return false;
      }
    },
    removerProducto(producto) {
      this.carrito =  this.carrito.filter( item=> item.id != producto.id);
    },
    pagar(){
      this.carrito = [],
      alert("Venta completada");
    }
  },
};
</script>

<style>
</style>

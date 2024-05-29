<template>
  <div id="card__person" class="container my-5">
    <div class="card" style="width: ">
      <img :src="usuario.picture.large" class="card-img-top" alt="" />
      <div class="card-body">
        <h5 class="card-title">{{ nombreCompleto }}</h5>
        <form>
          <input
            class="form-control my-2"
            type="color"
            name="color"
            id="color"
            v-model="mensaje.color"
          />
          <textarea
            class="form-control my-2"
            name="chat"
            id="chat"
            v-model="mensaje.texto"
            @keyup.enter="enviarMensaje"
          ></textarea>
          <!-- Tenemos que hacer un emit para enviar del hijo al padre -->

          <button @click.prevent="enviarMensaje" class="btn">Enviar</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardPerson",
  // Props es para recibir desde el padre, ahí queda registrada y queda disponible como si la tuviera dentro de data()
  props: {
    usuario: Object,
  },
  //
  data() {
    return {
      mensaje: {
        texto: "",
        color: "#fff",
        id: "",
      },
    };
  },
  computed: {
    nombreCompleto() {
      return `${this.usuario.name.first} ${this.usuario.name.last}`;
    },
  },
  methods: {
    enviarMensaje() {
      this.mensaje.id = this.usuario.id.value;
      this.mensaje.nombreCompleto = this.nombreCompleto;
      this.$emit("enviarMensaje", this.mensaje);
      this.mensaje.texto = "";
    },
  },
  created() {
    console.log(this.usuario);
  },
};
</script>

<style scoped>
.card-body {
  color: rgb(133, 123, 35);
}
.btn {
  color: rgb(53, 56, 40);
  background-color: rgb(219, 200, 160);
}
</style>

<template>
  <div id="app">
    <!-- Aca ingresamos los props que es pasarle del padre al hijo -->
    <h1 class="text-center my-5">Chat Randomuser</h1>
    <main class="my-5 container">
      <div class="row">
        <div class="col-3">
          <CardPerson
            :usuario="usuarios[0]"
            @enviarMensaje="enviarMensajeHandler"
          />
        </div>
        <div class="col-6">
          <ChatUsers :mensajes="mensajes" :usuarios="usuarios" />
          <!-- chatbox -->
        </div>
        <div class="col-3">
          <CardPerson
            :usuario="usuarios[1]"
            @enviarMensaje="enviarMensajeHandler"
          />
        </div>
      </div>
      
    </main>
    <div>
  <footer class="text-center">
<h2>ChatRandomUsers - Beatriz Taborda A. 
Junio 2024.
</h2>
</footer>
</div>

  </div>
  
</template>


<script>
import axios from "axios";
import CardPerson from "./components/CardPerson.vue";
import ChatUsers from "./components/ChatUsers.vue";

export default {
  name: "App",
  components: {
    CardPerson,
    ChatUsers,
  },

  data() {
    return {
      usuarios: [],
      mensajes: [],
    };
  },
  // este método es el que llama a la información de la api, por eso usamos axios.get
  methods: {
    async getPerson() {
      try {
        let response = await axios.get("https://randomuser.me/api/?results=2");
        this.usuarios = response.data.results;
      } catch (error) {
        console.log(error);
      }
    },
    enviarMensajeHandler(mensaje) {
            let nuevoMensaje = {
                id: mensaje.id,
                color: mensaje.color,
                nombreCompleto: mensaje.nombreCompleto,
                texto: mensaje.texto
            }
            this.mensajes.push(nuevoMensaje)
        }
  },
  // Metodo de ciclo de vida, le estoy diciendo a la app.vue, a penas me monte el dom ejecute la funcion getPerson
  mounted() {
    this.getPerson();
  },
};
</script>

<style scoped>
#app{
font-family: "Edu TAS Beginner", cursive;
color: rgb(53, 56, 40);
background-color: rgb(172, 167, 167);

}
h1{
  color: rgb(53, 56, 40);
}

</style>

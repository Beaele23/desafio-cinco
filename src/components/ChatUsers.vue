<template>
    <div class="container my-5" id="chat">
        <div v-for="(mensaje, index) in mensajes" :key="index">
            <p
                :style="{ textAlign: mensaje.id === usuarios[0].id.value ? 'left' : 'right' }">
                <small>{{ mensaje.nombreCompleto }}</small>
            </p>
            <p
                :style="{ backgroundColor: mensaje.color, textAlign: mensaje.id === usuarios[0].id.value ? 'left' : 'right' }">
                {{ mensaje.texto
                }}
            </p>
        </div>
    </div>
</template>
<script>
export default {
  name: "ChatUsers",
  props: {
    mensajes: Array,
    usuarios: Array,
  },
 
};
</script>
<style scoped>
#chat{
    max-height: 75vh;
    overflow-y: scroll;
   
}
.container{
background: rgb(219, 200, 160);

border-radius: 20px;
}

</style>
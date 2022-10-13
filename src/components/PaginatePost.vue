<script setup>
defineProps(["inicio", "fin", "maxLength"])

const emit = defineEmits(["cambioNext","cambioPrev"]);

const activarSiguiente = () =>{
    console.log("me diste siguiente");
    emit("cambioNext");
};
</script>

<template>
<div class="btn-group" role="group" aria-label="Basic example">
  <button 
     @click="emit('cambioPrev')"
     type="button"  
     class="btn btn-outline-primary"
     :disabled="inicio === 0"
   >
   Left
</button>
  <button
     @click="activarSiguiente"  
     type="button" 
     class="btn btn-outline-primary"
     :disabled="fin >= maxLength"
   >
   Right
</button>
</div>

</template>

<template>
    <div class="form">
        <label>Изменить радиус окружности</label>
        <input type="text" placeholder="Радиус окружности" v-model="configCircle.radius"/>
        <label>Изменить высоту квадрата</label>
        <input type="text" placeholder="Сторона квадрата" v-model="configRect.height"/>
        <label>Изменить ширину квадрата</label>
        <input type="text" placeholder="Сторона квадрата" v-model="configRect.width"/>
    </div>
    <v-stage :config="configKonva">
    <v-layer>
      <v-circle :config="configCircle">
        
    </v-circle>
    <v-rect :config="configRect"></v-rect>
    </v-layer>
  </v-stage>
</template>

<script setup>
import { onUpdated, reactive, ref } from 'vue';

onUpdated(() =>{
    if(configCircle.radius < configRect.value.height || configCircle.value.radius < configRect.value.height){
        configCircle.value.radius = configRect.value.height;
    }
})

const configKonva = ref({width: 1000, height: 1000})

const configCircle = ref({x: 300, y: 300, radius: 100, fill: "transparent", stroke: "black", strokeWidth: 4})

const configRect = ref({x: 300,
        y: 300,
        width: 100,
        height: 100,
        fill: 'green',
        stroke: 'black',
        strokeWidth: 4,
        draggable: true})
</script>

<style lang="scss" scoped>
.form{
    display: flex;
    flex-direction: column;
    justify-content: center;
    gap: 10px;

    input{
        max-width: 200px;
    }
}
</style>
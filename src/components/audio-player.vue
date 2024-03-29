<template>
    <div ref="audioContainer"></div>
    <div>currentTime：{{ currentTime }}</div>
</template>

<script setup lang="ts">
import WaveSurfer from 'wavesurfer.js';
import { onMounted, ref, onBeforeUnmount, getCurrentInstance } from 'vue';

const instance = getCurrentInstance();
const audioContainer = ref();
let wavesurfer;
let timer = 0;
let currentTime = ref(0);

const startInterval = () => {
    timer && clearInterval(timer);
    timer = setInterval(() => {
        currentTime.value = wavesurfer.getCurrentTime();
        console.log(`interval..., _uid=${instance.uid}`);
    }, 300);
};

onMounted(() => {
    console.log(`onMounted, _uid=${instance.uid}`);
    wavesurfer = WaveSurfer.create({
        container: audioContainer.value,
        progressColor: '#ff8000',
        cursorColor: '#ff8000',
        height: 58,
        barWidth: 3,
    });
    wavesurfer.load(
        'https://cdn.freesound.org/previews/729/729429_5674468-lq.mp3',
    );

    wavesurfer.on('ready', () => {
        console.log(`wavesurfer ready, startInterval..., _uid=${instance.uid}`);
        startInterval();
    });
});

onBeforeUnmount(() => {
    console.log(`onBeforeUnmount, _uid=${instance.uid}`);
    clearInterval(timer);
    timer = 0;
    wavesurfer && wavesurfer.destroy();
});
</script>

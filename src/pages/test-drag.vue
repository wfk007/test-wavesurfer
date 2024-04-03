<template>
    <div>test dragToSeek option</div>
    <div ref="audioContainer"></div>
</template>

<script setup lang="ts">
import WaveSurfer from 'wavesurfer.js';
import { onMounted, ref, onBeforeUnmount } from 'vue';

const audioContainer = ref();
let wavesurfer;

onMounted(() => {
    wavesurfer = WaveSurfer.create({
        container: audioContainer.value,
        progressColor: '#ff8000',
        cursorColor: '#ff8000',
        height: 58,
        barWidth: 3,
        dragToSeek: true,
    });
    wavesurfer.load(
        'https://cdn.freesound.org/previews/729/729429_5674468-lq.mp3',
    );
});

onBeforeUnmount(() => {
    wavesurfer && wavesurfer.destroy();
});
</script>

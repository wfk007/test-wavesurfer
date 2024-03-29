<template>
    <div>
        <h2>test wavesurfer memory leak</h2>
        <audio-player v-if="showAudioPlayer"></audio-player>
    </div>
</template>

<script setup lang="ts">
import { onMounted, ref, onBeforeUnmount, nextTick } from 'vue';
import AudioPlayer from '@/components/audio-player.vue';

const showAudioPlayer = ref(true);

onMounted(() => {
    // in some conditions, component will be mounted twice or more
    nextTick(() => {
        showAudioPlayer.value = false;
        nextTick(() => {
            showAudioPlayer.value = true;
        });
    });
});
</script>

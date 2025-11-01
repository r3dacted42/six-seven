<script setup lang="ts">
import { useParallax } from '@vueuse/core';
import { computed, type CSSProperties, useTemplateRef } from 'vue';

const container = useTemplateRef("container");
const { tilt, roll } = useParallax(container);
const factor = 20;

const leftHandStyle = computed<CSSProperties>(() => ({
    transform: `translateY(${tilt.value * factor}%)`,
}));
const rightHandStyle = computed<CSSProperties>(() => ({
    transform: `translateY(${-tilt.value * factor}%)`,
}));
</script>

<template>
    <div ref="container" class="container">
        <div class="scp">
            <img :style="leftHandStyle" class="left" src="/hand_left.png" />
            <img :style="rightHandStyle" class="right" src="/hand_right.png" />
        </div>
    </div>
</template>

<style scoped>
.container {
    height: 100%;
    display: flex;
    place-content: center;
    --hand-top: 50%;

    * {
        min-width: 0;
    }
}

.scp {
    width: 100%;
    height: auto;
    aspect-ratio: 16 / 9;
    position: relative;
    background-image: url(/scp.png);
    background-repeat: no-repeat;
    background-position: center;
    background-size: contain;
}

.left {
    position: absolute;
    left: 0;
    top: var(--hand-top);
    width: 45%;
}
.right {
    position: absolute;
    right: 0;
    top: var(--hand-top);
    width: 45%;
}
</style>

<script setup lang="ts">
import { useParallax } from '@vueuse/core';
import { computed, type CSSProperties, useTemplateRef } from 'vue';

const container = useTemplateRef("scp");
const { tilt, source } = useParallax(container);

const factor = computed(() => {
    if (source.value === 'deviceOrientation') return 50;
    return 30;
});

const leftHandStyle = computed<CSSProperties>(() => ({
    transform: `translateY(${tilt.value * factor.value}%)`,
}));
const rightHandStyle = computed<CSSProperties>(() => ({
    transform: `translateY(${-tilt.value * factor.value}%)`,
}));
</script>

<template>
    <div ref="scp" class="scp">
        <img :style="leftHandStyle" style="left: 0;" src="/hand_left.png" />
        <img :style="rightHandStyle" style="right: 0;" src="/hand_right.png" />
    </div>
</template>

<style scoped>
.scp {
    height: 100%;
    width: 100%;
    position: relative;
    background-image: url(/scp.png);
    background-repeat: no-repeat;
    background-position: center;
    background-size: contain;

    img {
        position: absolute;
        top: 50%;
        width: 45%;
    }
}
</style>

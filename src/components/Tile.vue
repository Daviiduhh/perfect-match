<template>
    <div class="tile" :style="visible ? background(color) : background('#9670c9')">
        <img v-show="visible" class="tile__icon" :src="icon" :alt="'Imagen de ' + name">
    </div>
</template>

<script setup>
import { computed, ref } from '@vue/reactivity';

const props = defineProps({
  icon: String,
  color: String,
  visible: Boolean,
  name: String
})

const background = ((color) => {
    return 'background-color: ' + color + ';'
}) 
</script>

<style lang="scss" scoped>
    .tile {
        width: 6rem;
        aspect-ratio: 1;
        border: 3px solid #fff;
        border-radius: 1rem;
        display: flex;
        align-items: center;
        justify-content: center;
        background-color: var(--color);
        cursor: pointer;

        &__icon {
            width: 4rem;
            max-height: 5rem;
        }

        &:active {
            transform: scale(0.9);
        }
    }
</style>
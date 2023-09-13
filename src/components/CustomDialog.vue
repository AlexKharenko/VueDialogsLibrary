<template>
  <transition name="dialog">
    <div v-if="visible" class="dialog">
      <div class="dialog-content">
        <slot />
      </div>
      <div class="dialog-bg" @click="hide"></div>
    </div>
  </transition>
</template>

<script setup lang="ts">
import { ref } from "vue";

const visible = ref<boolean>(false);

const show = (): void => {
  visible.value = true;
};

const hide = (): void => {
  visible.value = false;
};

defineExpose({ show, hide });
</script>

<style lang="scss"></style>

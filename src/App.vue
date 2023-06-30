<template>
  <AlertDialog ref="alertDialogRef" />
  <ConfirmDialog btn-ok-text="Yes" btn-cancel-text="No" :alert="false" ref="confirmDialogRef" />
  <button @click="showCustomAlert">Show Custom Alert</button>
  <button @click="showCustomConfirm">Show Custom Confirm</button>
</template>

<script setup lang="ts">
import { ref } from "vue";
import AlertDialog from "./components/AlertDialog.vue";
import ConfirmDialog from "./components/ConfirmDialog.vue";

const alertDialogRef = ref<InstanceType<typeof AlertDialog>>();
const confirmDialogRef = ref<InstanceType<typeof ConfirmDialog>>();

const showCustomAlert = async (): Promise<void> => {
  const result = await alertDialogRef.value?.show(
    "Ooops, something went wrong!"
  );
  console.log(result);
};

const showCustomConfirm = async (): Promise<void> => {
  const result = await confirmDialogRef.value?.show("Are you ready?");
  console.log(result);
};
</script>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>

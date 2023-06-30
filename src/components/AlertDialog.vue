<template>
  <transition name="dialog">
    <div v-if="visible" class="dialog alert-dialog">
      <div class="dialog-content">
        <div class="dialog-header">
          <img class="img-alert" src="../assets/alert.svg" alt="Alert image" />
          <h3 class="header-text">{{ dialogTitle }}</h3>
        </div>
        <div class="dialog-body">
          <p>{{ message }}</p>
        </div>
        <div class="buttons-container">
          <button class="dialog-btn btn-ok" @click="handleOk">
            {{ btnOkText }}
          </button>
        </div>
      </div>
      <div class="dialog-bg"></div>
    </div>
  </transition>
</template>

<script setup lang="ts">
import "../styles/dialog.scss";
import { computed, ref } from "vue";

const visible = ref<boolean>(false);
const message = ref<string>("");
let resolve: ((value: boolean) => void) | null = null;

const props = defineProps<{
  title?: string;
  btnOkText?: string;
}>();
const dialogTitle = computed<string>(() => props.title || "Alert");
const btnOkText = computed<string>(() => props.btnOkText || "OK");

function show(dialogMessage: string): Promise<boolean> {
  message.value = dialogMessage;
  visible.value = true;

  return new Promise<boolean>((res) => {
    resolve = res;
  });
}

const hideDialog = () => {
  visible.value = false;
};

const handleOk = () => {
  hideDialog();
  if (resolve) {
    resolve(true);
  }
};

defineExpose({ show });
</script>

<style lang="scss"></style>

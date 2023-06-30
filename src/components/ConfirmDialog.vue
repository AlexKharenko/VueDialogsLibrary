<template>
  <transition name="dialog">
    <div v-if="visible" class="dialog">
      <div class="dialog-content">
        <div class="dialog-header" :class="{ 'border-btm-alert': alert }">
          <img
            :class="alert ? 'img-alert' : 'img-attention'"
            src="../assets/alert.svg"
            alt="Alert image"
          />
          <h3 class="header-text">{{ dialogTitle }}</h3>
        </div>
        <div class="dialog-body">
          <p>{{ message }}</p>
        </div>
        <div class="buttons-container">
          <button
            class="dialog-btn"
            :class="alert ? 'btn-alert' : 'btn-ok'"
            @click="handleOk"
          >
            {{ btnOkText }}
          </button>
          <button class="dialog-btn" @click="handleCancel">
            {{ btnCancelText }}
          </button>
        </div>
      </div>
      <div class="dialog-bg" @click="handleCancel"></div>
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
  alert?: boolean;
  btnOkText?: string;
  btnCancelText?: string;
}>();

const dialogTitle = computed<string>(() => props.title || "Confirm");
const btnOkText = computed<string>(() => props.btnOkText || "Confirm");
const btnCancelText = computed<string>(() => props.btnCancelText || "Cancel");

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

const handleCancel = () => {
  hideDialog();
  if (resolve) {
    resolve(false);
  }
};

defineExpose({ show });
</script>

<style></style>

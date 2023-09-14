# Vue dialogs library

It allows you to call the dialog from code like ```window.alert()``` and wait for user's answer. 

* Vue3 based component.

## Instalation

### npm
```
npm install vue-dialog-library
```

## Usage

You can use it locally.

### Locally

* component.vue

```
import "vue-dialog-library/dist/styles.css";
import { AlertDialog } from "vue-dialog-library";


const alertDialogRef = ref<InstanceType<typeof AlertDialog>>();

const showCustomAlert = async (): Promise<void> => {
  // Your code
  const result = await alertDialogRef.value?.show(
    "Ooops, something went wrong!"
  );
  // Your code
};
```

```
<template>
  <AlertDialog :title="'ok'" ref="alertDialogRef" />
</template>
```

## Props

* Alert dialog

| Name          | Type    | Default            | Description                     |
| ------------- | ------- | ------------------ | ------------------------------- |
| title         | String  | Alert              | Title on the top side of dialog |
| btnOkText     | String  | OK                 | Text on button                  |


* Confirm dialog

| Name          | Type    | Default            | Description                     |
| ------------- |-------- | ------------------ | ------------------------------- |
| title         | String  | Confirm            | Title on the top side of dialog |
| btnOkText     | String  | Confirm            | Text on button                  |
| btnCancelText | String  | Cancel             | Text on button                  |
| alert         | Boolean | false              | Styling property                |
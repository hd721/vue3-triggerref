<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <button @click="onChangeAndTrigger">Click me!</button>
  <button @click="onShow">Print the current value</button>
</template>

<script lang="ts">
import { shallowRef, watch, triggerRef } from "vue";
export default {
  name: "App",
  setup() {
    let shallow = shallowRef({
      greet: "World",
    });

    watch(shallow, (value) => {
      console.log("Hello,", value.greet);
    });

    const onChangeAndTrigger = () => {
      // No action happens after this because the ref is shallow
      shallow.value.greet = "Universe";

      // Watch should be triggered?
      triggerRef(shallow);
    };

    const onShow = () => {
      console.log("Current value:", shallow.value.greet);
    };

    return {
      onChangeAndTrigger,
      onShow,
    };
  },
};
</script>

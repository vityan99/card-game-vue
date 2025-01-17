<script lang="ts">
import { defineComponent } from "vue";
import type { PropType } from "vue";

export default defineComponent({
  name: "Button",
  props: {
    title: {
      type: String as PropType<string>,
      required: true,
    },
    use: {
      type: String as PropType<string>,
      required: true,
    },
    size: {
      type: String as PropType<string>,
      required: false,
    },
    clickHandler: {
      type: Function as PropType<() => void>,
      required: true,
    },
    disabled: {
      type: Boolean as PropType<boolean>,
      required: false,
    },
  },
  components: {},
  setup(props) {
    const sizeModificator = props.size && props.size !== "small" ? `btn--${props.size}` : "";

    return {
      ...props,
      sizeModificator,
    };
  },
});
</script>

<template>
  <button :class="['btn', use ? `btn--${use}` : '', sizeModificator]" @click="clickHandler" :disabled="disabled">{{ title }}</button>
</template>

<style scoped>
.btn {
  margin: 0;
  padding: 0;
  border: none;
  background-color: transparent;
  border: 1px solid #cecece;
  border-radius: 7px;
  padding: 7px 10px;
  cursor: pointer;
}

.btn:hover {
  opacity: 0.9;
}

.btn--primary {
  background-color: rgb(47, 47, 47);
  color: #fff;
  border: none;
}

.btn--success {
  background-color: yellowgreen;
  color: #fff;
  border: none;
}

.btn--danger {
  background-color: tomato;
  color: #fff;
  border: none;
}

.btn--pay {
  background-color: rgb(255, 98, 0);
  color: #000;
  border: none;
}

.btn--text {
  background-color: transparent;
  color: #000;
  border: none;
}

.btn--link {
  background-color: transparent;
  color: #000;
  border: none;
  text-decoration: underline;
  text-underline-offset: 3px;
}

.btn--medium {
  font-size: 18px;
}

.btn--large {
  padding: 8px 18px;
  font-size: 18px;
}

button:disabled {
  border: 2px solid red;
}
</style>

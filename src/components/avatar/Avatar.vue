<script lang="ts">
import { defineComponent, type PropType } from "vue";

export default defineComponent({
  name: "Avatar",
  props: {
    img: {
      type: String as PropType<string>,
      required: true,
    },
  },
  setup(props) {
    return {
      ...props,
    };
  },
});
</script>

<template>
  <img class="avatar" alt="avatar" :src="img" />
</template>

<style scoped>
.avatar {
  width: 100%;
  height: 100%;
  border-radius: 100%;
  object-fit: cover;
}
</style>

<script lang="ts">
import { computed, defineComponent, type PropType } from "vue";

export default defineComponent({
  name: "UsersOnline",
  props: {
    usersOnline: {
      type: Number as PropType<number>,
      reuqired: true,
    },
  },
  setup(props) {
    const updatedUsersOnline = computed(() => props.usersOnline);

    return {
      ...props,
      updatedUsersOnline,
    };
  },
});
</script>

<template>
  <span>Сейчас пользователей онлайн: {{ updatedUsersOnline }}</span>
</template>

<style scoped></style>

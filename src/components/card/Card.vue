<script lang="ts">
import { computed, defineComponent, type PropType } from "vue";

import type { UserType } from "@/assets/types/types";

import Avatar from "../avatar/Avatar.vue";

export default defineComponent({
  name: "Card",
  props: {
    user: {
      type: Object as PropType<UserType>,
      required: true,
    },
    selectedId: {
      type: Boolean as PropType<boolean>,
      required: true,
    },
    handler: {
      type: Function as PropType<(id: number) => void>,
      required: true,
    },
  },
  components: {
    Avatar,
  },
  setup(props) {
    const updatedSelectedId = computed(() => props.selectedId);

    return {
      ...props,
      updatedSelectedId,
    };
  },
});
</script>

<template>
  <div :class="updatedSelectedId ? 'card' : 'card--not-active'" @click="() => handler(user.id)">
    <div
      :class="[
        'card__img-wrapper',
        {
          'user--online': user.online,
        },
      ]"
    >
      <Avatar :img="user.avatar" />
    </div>
    <span class="card__username">{{ user.name }}</span>
    <span class="card__money">{{ user.money }} руб.</span>
  </div>
</template>

<style scoped>
.card {
  padding: 5px;
  width: 200px;
  background-color: rgb(74, 74, 235);
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  cursor: pointer;
  box-shadow: 6px 6px 10px 3px rgba(34, 60, 80, 0.2);
}

.card--not-active {
  padding: 5px;
  width: 200px;
  background-color: rgb(144, 144, 251);
  border-radius: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  cursor: pointer;
  box-shadow: 6px 6px 10px 3px rgba(34, 60, 80, 0.2);
}

.card__img-wrapper {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  position: relative;
}

.user--online::after {
  content: "";
  position: absolute;
  top: 5px;
  right: 5px;
  width: 15px;
  height: 15px;
  background-color: rgb(0, 255, 0);
  border-radius: 50%;
  border: 2px solid white;
}

.card__username,
.card__money {
  color: #fff;
}
</style>

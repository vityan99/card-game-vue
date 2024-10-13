<script lang="ts">
import { defineComponent, onMounted, watch, computed } from "vue";

import type { PropType } from "vue";
import type { UserType } from "@/assets/types/types";

import { selectedId, setSelectedId, clickedGo, setClickedGo, timeOut, setTimeOutValue, usersOnline } from "@/assets/store/store.vue";
import UsersOnline from "../usersOnline/UsersOnline.vue";
import Button from "../button/Button.vue";
import Card from "../card/Card.vue";

export default defineComponent({
  name: "UserCards",
  props: {
    users: {
      type: Array as PropType<UserType[]>,
      required: true,
    },
    gameMoney: {
      type: Number as PropType<number>,
      required: true,
    },
    handler: {
      type: Function as PropType<(id: number) => void>,
      required: true,
    },
  },
  components: {
    UsersOnline,
    Button,
    Card,
  },
  setup(props) {
    const getUsersOnline = (): void => {
      usersOnline.value = props.users.length;
    };

    const startGameHandler = (): void => {
      setClickedGo(!clickedGo.value);
      setTimeOutValue(parseInt((Math.random() * (8 - 2) + 2).toFixed(0)) * 1000);
    };

    const setSelectedIdHandler = (id: number): void => {
      selectedId.value === id ? setSelectedId(-1) : setSelectedId(id);
    };

    const gameMoneyHandler = (): void => {
      if (props.gameMoney > 0) {
        props.handler(selectedId.value);
      }
    };

    onMounted(() => {
      getUsersOnline();
    });

    watch(
      () => props.users.length,
      () => getUsersOnline()
    );

    watch([() => clickedGo.value, () => timeOut.value], (newValues) => {
      const [isClicked, timeout] = newValues;

      if (isClicked) {
        const timeoutId = setTimeout(() => {
          setClickedGo(false);
        }, timeout);

        return () => clearTimeout(timeoutId);
      }
    });

    return {
      usersOnline,
      startGameHandler,
      setSelectedIdHandler,
      gameMoneyHandler,
      clickedGo,
      selectedId,
    };
  },
});
</script>

<template>
  <div class="user-cards">
    <div class="game-controllers">
      <UsersOnline :usersOnline="usersOnline" />
      <span class="game-money">{{ gameMoney }} руб.</span>
      <Button title="Начать игру" use="primary" :clickHandler="startGameHandler" />
      <Button
        v-if="clickedGo && selectedId !== -1"
        title="Забрать деньги"
        use="success"
        :clickHandler="gameMoneyHandler"
        :disabled="gameMoney === 0"
      />
    </div>
    <div class="users">
      <Card v-for="user in users" :key="user.id" :user="user" :selectedId="user.id === selectedId" :handler="setSelectedIdHandler" />
    </div>
  </div>
</template>

<style scoped>
.user-cards {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 50px;
  flex-direction: column;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  margin: 0;
}

.game-controllers {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}

.users {
  display: flex;
  gap: 100px;
  align-items: center;
}
</style>

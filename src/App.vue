<script lang="ts">
import { defineComponent } from "vue";

import { store, gameMoney, incrementUserMoney, decrementGameMoney } from "./assets/store/store.vue";
import UserCards from "./components/userCards/UserCards.vue";

export default defineComponent({
  name: "App",
  components: {
    UserCards,
  },
  setup() {
    const setGameAndUserMoneyHandler = (id: number): void => {
      if (gameMoney.value >= 10) {
        decrementGameMoney(10);
        incrementUserMoney(id);
      }
    };

    return {
      ...store,
      gameMoney,
      setGameAndUserMoneyHandler,
    };
  },
});
</script>

<template><UserCards :users="users" :gameMoney="gameMoney" :handler="setGameAndUserMoneyHandler" /></template>

<style scoped></style>

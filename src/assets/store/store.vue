<script lang="ts">
import { reactive, ref } from "vue";

export const store = reactive({
  users: [
    {
      id: 1,
      name: "Jack",
      avatar: "https://cdn0.iconfinder.com/data/icons/team-work-and-organization-2/128/78-1024.png",
      money: 0,
      online: true,
    },
    {
      id: 2,
      name: "Mark",
      avatar: "https://i.pinimg.com/originals/f4/f3/dd/f4f3dd7acfd64b16aa51027159a6f5e8.png",
      money: 0,
      online: true,
    },
  ],
});

export const gameMoney = ref(100);
export const selectedId = ref(-1);
export const clickedGo = ref(false);
export const timeOut = ref(0);
export const usersOnline = ref(0);

export const incrementUserMoney = (id: number): void => {
  const user = store.users.find((user) => user.id === id);

  if (user) {
    user.money += 10;
  }
};

export const decrementGameMoney = (value: number): void => {
  gameMoney.value -= value;
};

export const setSelectedId = (id: number): void => {
  selectedId.value = id;
};

export const setClickedGo = (value: boolean): void => {
  clickedGo.value = value;
};

export const setTimeOutValue = (value: number): void => {
  timeOut.value = value;
};
</script>

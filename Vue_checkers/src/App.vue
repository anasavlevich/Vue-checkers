<template>
  <div class="app">
    <div class="app__container">
      <UserInfo :user="userStore.userWhite" class="app__user" :isActive="currentPlayer === 1" />
      <CheckersTable class="app__table" />
      <UserInfo :user="userStore.userBlack" class="app__user" :isActive="currentPlayer === 2" />
    </div>
  </div>
</template>

<script setup>
import { computed } from "vue";
import CheckersTable from "@/components/CheckersTable.vue";
import UserInfo from "@/components/userInfo.vue";
import { useUserStore } from "@/store/user";
import { useMainStore } from "@/store";

const store = useMainStore();
const currentPlayer = computed(() => store.currentPlayer);
const userStore = useUserStore();
</script>

<style lang="less">
.app {
  display: flex;
  flex-direction: column;
  margin: 0 auto;
  width: 1400px;
  align-items: center;

  &__container {
    display: flex;
  }
}
</style>
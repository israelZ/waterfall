<template>
  <div v-if="drinkSelecte" class="container-drink">
    <img :src="drinkSelecte.strDrinkThumb" />
    <span class="desc">{{ drinkSelecte.strInstructions }}</span>
    <div class="container-details">
      <span>{{ drinkSelecte.strDrink }}</span>
      <span>{{ drinkSelecte.strCategory }}</span>
      <span>{{ drinkSelecte.strGlass }}</span>
    </div>
  </div>
  <span v-else class="not-select">not Select Drink</span>
</template>




<script>
import { bus } from "../main";

export default {
  name: "drink-select",
  props: {
    drinkSelecte: {
      type: Object,
    },
  },
  data() {
    return {};
  },
  methods: {},
  created() {
    bus.$on("resultSearch", (drink) => {
      this.drinkSelect = drink;
    });
  },
};
</script>

<style scoped>
.container-drink{
    width: 50vw;
}
img {
  width: 100%;
}
.container-details {
  display: flex;
  flex-direction: column;
}
.desc {
  font-size: 20px;
}
.not-select {
  width: 50vw;
  text-align: center;
  font-size: 60px;
      align-self: center;
}
@media screen and (max-width: 600px) {
  .container-drink {
    width: unset;
    display: flex;
    flex-direction: column;
    align-items: center;
    height: 50vh;
    overflow-y: auto;
    border: 1px solid black;
    border-radius: 20px;

  }
  .not-select{
      height: 50vh;
  }
  img {
    width : 60%;
  }
}
</style>

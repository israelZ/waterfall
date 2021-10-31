<template>
  <span id="continer">
    <div class="continer">
      <div
        v-for="drink in containerResultsDrink"
        :key="drink.idDrink"
        class="card"
        v-on:click="onClickDrink(drink.idDrink)"
      >
        <img :src="drink.strDrinkThumb" />
        <div class="details">
          <span>{{ drink.strDrink }}</span>
          <span>{{ drink.strCategory }}</span>
          <span>{{ drink.strGlass }}</span>
        </div>
      </div>
    </div>
  </span>
</template>




<script>
import { bus } from "../main";

export default {
  name: "continer",
    props:{
      drinkSelecte:{
          type:Function,
          require:true
      }
  },
  data() {
    return {
      inputSerch: "",
      containerResultsDrink: [],
      idDrink: "",
    };
  },
  methods: {
    onClickDrink: function (idDrink) {
      this.drinkSelecte(idDrink)
    },
  },

  created() {
    bus.$on("resultSearch", (result) => {
      this.containerResultsDrink = result;
    });

    for (let index = 0; index < 10; index++) {
      this.$http
        .get(`https://www.thecocktaildb.com/api/json/v1/1/random.php`)
        .then((res) => {
          if (res.body.drinks) {
            this.containerResultsDrink.push(res.body.drinks[0]);
          }
        },
        (error)=>{console.error(error)});
    }
  },
};


</script>

<style scoped>
.card {
  display: flex;
  position: relative;
  height: 25vh;
  border: solid 2px black;
  border-radius: 10px;
  margin: 10px;
}
img {
  height: 100%;
    width: auto;
}
#continer {
  display: flex;
  flex-direction: column;
  width: 50vw;
  height: 100vh;
  overflow-y: auto;
  padding: 10px;
}
.ingredients {
  position: absolute;
  top: 10px;
  width: 100%;
  text-align: center;
}
.details {
  display: grid;
  justify-items: center;
  width: 100%;
  align-items: center;
}
@media screen and (max-width: 600px) {
  #continer{
    width: 100%;
  }
}
</style>

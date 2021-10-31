<template>
  <div id="app">
    <meta name="viewport" content="width=device-width,initial-scale=1.0">
    <search-drink></search-drink>
    <div class="container-results">
      <continer v-bind:drinkSelecte="slectedDrink"></continer>
      <drink-select v-bind:drinkSelecte="drinkSelecte"></drink-select>
    </div>
  </div>
</template>

<script>
import Continer from "./component/Continer.vue";
import SearchDrink from "./component/SearchDrink.vue";
import DrinkSelect from "./component/DrinkSelect.vue";

export default {
  name: "app",
  components: {
    Continer,
    SearchDrink,
    DrinkSelect,
  },
  data() {
    return {
      drinkSelecte:null
    };
  },
  methods:{
    getDrink: function (idDrink) {
      return this.$http.get(
        `https://www.thecocktaildb.com/api/json/v1/1/lookup.php?i=${idDrink}`
      );
    },
    slectedDrink(idDrink){
      this.getDrink(idDrink).then(res=>{
        if (res.body.drinks) {
          this.drinkSelecte=res.body.drinks[0]
        }
      },
      (error)=>{console.error(error)})
    }
  }
};
</script>

<style scoped>
.container-results{
  display: flex;
}
@media screen and (max-width: 600px) {
  .container-results{
    flex-direction: column-reverse;
  }
}
</style>

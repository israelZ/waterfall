<template>
  <div>
    <form>
      <input type="text" v-model="inputSearch" />
      <button v-on:click.prevent="getDrink">Search</button>
    </form>
    <div>
    History Serch:
    <button
      v-for="(history, i) in historySearch"
      :key="i"
      v-on:click="getDrinkByHistory(history)"
    >
      {{ history }}
    </button>
    </div>
  </div>
</template>




<script>
import { bus } from "../main";

export default {
  name: "search-drink",
  data() {
    return {
      inputSearch: "",
      historySearch: [],
    };
  },
  methods: {
    getDrink: function () {
      const { inputSearch, historySearch } = this;

      if (!historySearch.includes(inputSearch)) {
        historySearch.push(inputSearch);
      }

      this.$http
        .get(
          `https://www.thecocktaildb.com/api/json/v1/1/search.php?s=${inputSearch}`
        )
        .then(
          (res) => {
            if (res.body.drinks) {
              bus.$emit("resultSearch", res.body.drinks);
            }
          },
          (error) => {
            console.error(error);
          }
        );
    },
    getDrinkByHistory: function (value) {
      if (value != this.inputSearch) {
        this.inputSearch = value;
        this.getDrink();
      }
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
  justify-content: center;
  padding: 10px;
}
input {
  margin-right: 10px;
}
button{
  background: #0d6efd;
    border: 0px solid;
    border-radius: 3px;
    width: fit-content;
    padding: 2px 6px;
    font-size: 20px;
    margin: 0 2px;
    color: white;
    box-shadow: 1px 1px 3px 0px rgb(79 79 79 / 99%);
}
</style>

<template>
  <form>
    <input type="text" v-model="inputSerch" />
    <button v-on:click.prevent="getDrink">Search</button>
  </form>
</template>




<script>
import { bus } from "../main";

export default {
  name: "search-drink",
  data() {
    return {
      inputSerch: "",
    };
  },
  methods: {
    getDrink: function () {
      const { inputSerch } = this;

      this.$http
        .get(
          `https://www.thecocktaildb.com/api/json/v1/1/search.php?s=${inputSerch}`
        )
        .then((res) => {
          if (res.body.drinks) {
            bus.$emit("resultSearch", res.body.drinks);
          }
        },
        (error)=>{console.error(error)});
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
</style>

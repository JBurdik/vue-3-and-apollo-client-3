<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <HelloWorld msg="Welcome to Your Vue.js App" />
  {{ message }}
  <ul class="flex m-auto">
    <li v-for="burger in burgers" :key="burger.id">
      <h2>{{ burger.name }}</h2>
      <button @click="alert">
        delete this wine
      </button>
    </li>
  </ul>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import { ref } from "vue";
import { useQuery, useResult, useMutation } from "@vue/apollo-composable";
import allBurgersQuery from "./graphql/burgers.query.gql";

export default {
  name: "App",
  components: {
    HelloWorld
  },
  setup() {
    const message = ref("Hello Jason!");
    const { result } = useQuery(allBurgersQuery);
    const burgers = useResult(result, null, (data) => data.burgers);

    function alert() {
      console.log("hello there");
    }

    return { message, burgers, alert };
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

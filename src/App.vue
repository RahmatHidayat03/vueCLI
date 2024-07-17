<template>
  <div id="app" class="container mt-5">
    <h1>IDShop</h1>
    <p class="animate__animated animate__fadeInRight">
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Quae, quasi
      libero animi praesentium aliquam deleniti? Nostrum quasi aliquid culpa
      quisquam sint assumenda non, doloribus, quas quae ducimus cum repellat
      officia!
    </p>
    <Font-awesome-icon icon="shopping-cart"></Font-awesome-icon>
    <price :value="4.23"></price>
  </div>
</template>

<script>
import { FontAwesomeIcon } from "@fortawesome/vue-fontawesome";
import price from "./components/Price.vue";

export default {
  name: "App",
  components: {
    FontAwesomeIcon,
    price,
  },
};
</script>

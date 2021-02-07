<template>
  <div class="home">
    <Navbar />
    <div class="container">
      <Hero />
      <div class="row mt-4">
        <div class="col">
          <h2>Best <strong>Foods</strong></h2>
        </div>
        <div class="col">
          <router-link to="/foods" class="btn btn-success float-right"
            ><b-icon-eye></b-icon-eye> Semua</router-link
          >
        </div>
      </div>

      <div class="row mb-3">
        <!-- panggil data json pakai v-for(foreach) dan key untuk id nya -->
        <div
          class="col-md-4 mt-4"
          v-for="product in products"
          :key="product.id"
        >
          <h2>Makanan</h2>
          <!-- product ngambil alias dari div yang diatas -->
          <CardProduct :product="product" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Navbar from "@/components/Navbar.vue";
import Hero from "@/components/Hero.vue";
import CardProduct from "@/components/CardProduct.vue";

// pakai axios untuk import data json
import axios from "axios";

export default {
  name: "Home",
  components: {
    Navbar,
    Hero,
    CardProduct,
  },

  // panggil data json
  data() {
    return {
      products: [],
    };
  },

  methods: {
    setProduct(data) {
      this.products = data;
    },
  },

  mounted() {
    axios
      .get("http://localhost:3000/best-products")
      // handle success
        //  set data json
      .then((response) => this.setProduct(response.data))
      .catch(function (error) {
        // handle error
        console.log(error);
      });
  },
};
</script>

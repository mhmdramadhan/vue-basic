<template>
  <div>
    <Navbar />
    <div class="container">
      <h2 class="mt-4">Daftar <strong>Makanan</strong></h2>
      <div class="row mt-3">
        <div class="col">
          <form class="form-inline my-2 my-lg-0">
            <input
              v-model="search"
              class="form-control mr-sm-2"
              type="search"
              placeholder="Search"
              aria-label="Search"
              @keyup="searchFood"
            />
            <button disabled class="btn btn-outline-success my-2 my-sm-0" type="submit">
              Search
            </button>
          </form>
        </div>
      </div>
      <div class="row">
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
import CardProduct from "@/components/CardProduct.vue";

// pakai axios untuk import data json
import axios from "axios";

export default {
  name: "Foods",
  components: {
    Navbar,
    CardProduct,
  },

  // panggil data json
  data() {
    return {
      products: [],
      search: "",
    };
  },

  methods: {
    setProduct(data) {
      this.products = data;
    },
    // method search
    searchFood() {
      axios
        .get("http://localhost:3000/products?q="+this.search)
        // handle success
        //  set data json
        .then((response) => this.setProduct(response.data))
        .catch(function (error) {
          // handle error
          console.log(error);
        });
    },
  },

  mounted() {
    axios
      .get("http://localhost:3000/products")
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

<style></style>

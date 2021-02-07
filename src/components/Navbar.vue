<template>
  <nav class="navbar navbar-expand-lg navbar-light">
    <div class="container">
      <a class="navbar-brand" href="#">Kulineran</a>
      <button
        class="navbar-toggler"
        type="button"
        data-toggle="collapse"
        data-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>

      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item">
            <router-link class="nav-link" to="/"><span>Home</span></router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/Foods"
              ><span>Foods</span></router-link
            >
          </li>
        </ul>
        <ul class="navbar-nav ml-auto">
          <li class="nav-item">
            <router-link class="nav-link" to="/Keranjang">
              <span>Keranjang</span>
              <b-icon-bag></b-icon-bag>
              <span class="badge badge-success">{{
               updateKeranjang ? updateKeranjang.length : jumlah_pesanan.length
              }}</span>
            </router-link>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
import axios from "axios";

export default {
  name: "Navbar",
  data() {
    return {
      jumlah_pesanan: [],
    };
  },

  props:['updateKeranjang'],
  methods: {
    setJumlah(data) {
      this.jumlah_pesanan = data;
    },
  },

  mounted() {
    axios
      .get("http://localhost:3000/keranjangs")
      // handle success
      //  set data json
      .then((response) => this.setJumlah(response.data))
      .catch(function (error) {
        // handle error
        console.log(error);
      });
  },
};
</script>

<style></style>

<template>
  <div class="card shadow">
    <img
      :src="'../assets/image/' + product.gambar"
      class="card-img-top"
      alt="..."
    />
    <div class="card-body">
      <h5 class="card-title">{{ product.nama }}</h5>
      <div class="card-text">
        <span class="badge badge-info">Harga : Rp.{{ product.harga }},-</span>
        <div class="mb-3" v-if="product.is_ready === true">
          Tersedia lohh ayo pesan!!
        </div>
        <div class="mb-3" v-else>Mohon maaf sudah habis</div>
        <!-- if button -->
        <div class="" v-if="product.is_ready === true">
          <router-link :to="'/Foods/' + product.id" class="btn btn-success"
            ><b-icon-cart></b-icon-cart> Pesan</router-link
          >
        </div>
        <div class="mb-3" v-else>
          <div class="row ml-2">
            <span style="font-size: 20px">&#128542;</span>
            <span style="font-size: 20px">&#128079; maaf</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "CardProduct",

  // ambil data product dari home
  props: ["product"],
};
</script>

<style>
</style>
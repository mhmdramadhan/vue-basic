<template>
  <!-- dexktop -->
  <div class="hero">
    <div class="d-none d-md-block">
      <div class="row">
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2>
                <strong>Best Food Menu, </strong> <br />
                in Your Gadget
              </h2>
              <p>Ayo segera pilih dan pesan makanan favorite anda</p>
              <router-link to="/Foods" class="btn btn-lg btn-success">
                <b-icon-arrow-right></b-icon-arrow-right> Pesan Sekarang!!
              </router-link>
            </div>
          </div>
        </div>
        <div class="col-md-6">
          <img src="../assets/image/Hero.png" width="100%" alt="" />
        </div>
      </div>
    </div>

    <!-- dll -->
    <div class="d-sm-block d-md-none">
      <div class="row">
        <div class="col-md-6 mb-3">
          <img src="../assets/image/Hero.png" width="100%" alt="" />
        </div>
        <div class="col-md-6">
          <div class="d-flex h-100">
            <div class="justify-content-center align-self-center">
              <h2>
                <strong>Best Food Menu, </strong> <br />
                in Your Gadget
              </h2>
              <p>Ayo segera pilih dan pesan makanan favorite anda</p>
              <button class="btn btn-lg btn-success">
                <b-icon-arrow-right></b-icon-arrow-right> Pesan Sekarang!!
              </button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Hero",
};
</script>

<style>
</style>
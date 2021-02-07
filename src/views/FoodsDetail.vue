<template>
  <div class="foodsdetail">
    <Navbar />
    <div class="container">
      <!-- breadcrumb -->
      <div class="row mt-5">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/" class="text-dark">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/foods" class="text-dark">Foods</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">
                Pesan Makanan
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row">
        <div class="col-md-6">
          <img
            :src="'../assets/image/' + products.gambar"
            class="img-fluid shadow"
            alt="..."
          />
        </div>
        <div class="col-md-6">
          <h2>
            <strong>{{ products.nama }}</strong>
          </h2>
          <hr />
          <h4>
            Harga :
            <strong class="badge badge-info">Rp.{{ products.harga }},-</strong>
          </h4>
          <form v-on:submit.prevent>
            <div class="form-group">
              <label for="">Jumlah Pemesanan</label>
              <input
                type="number"
                name=""
                id=""
                class="form-control"
                v-model="pesan.jumlah_pemesanan"
              />
            </div>
            <div class="form-group">
              <label for="">Keterangan</label>
              <textarea
                name=""
                id=""
                class="form-control"
                placeholder="keterangan spt : pedes, nasi setengah.."
                v-model="pesan.keterangan"
              ></textarea>
            </div>
            <button type="submit" class="btn btn-success" @click="pemesanan">
              <b-icon-cart></b-icon-cart> Pesan
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";

// pakai axios untuk import data json
import axios from "axios";

export default {
  name: "FoodsDetail",
  components: {
    Navbar,
  },

  data() {
    return {
      products: [],
      search: "",
      pesan: {},
    };
  },

  methods: {
    setProduct(data) {
      this.products = data;
    },
    pemesanan() {
      if (this.pesan.jumlah_pemesanan) {
        this.pesan.products = this.products;
        axios
          .post("http://localhost:3000/keranjangs", this.pesan)
          .then(() => {
            this.$router.push({ path: "/keranjang" });
            this.$toast.success("Sukses Masuk Keranjang", {
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((err) => console.log(err));
      } else {
        this.$toast.warning("Harap isi pesanan terlebih dahuu", {
          type: "warning",
          position: "top",
          duration: 3000,
          dismissible: true,
        });
      }
    },
  },

  mounted() {
    axios
      .get("http://localhost:3000/products/" + this.$route.params.id)
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

<style>
</style>
<template>
  <div>
    <Navbar :updateKeranjang="keranjangs" />
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
                Keranjang
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <h2>Keranjang <strong>Saya</strong></h2>
          <div class="table-responsive mt-5">
            <table class="table">
              <thead>
                <tr>
                  <th scope="col">#</th>
                  <th scope="col">Foto</th>
                  <th scope="col">Makanan</th>
                  <th scope="col">Keterangan</th>
                  <th scope="col">jumlah</th>
                  <th scope="col">Harga</th>
                  <th scope="col">Total Harga</th>
                  <th scope="col">Hapus</th>
                </tr>
              </thead>
              <tbody>
                <tr
                  v-for="(keranjang, index) in keranjangs"
                  :key="keranjang.id"
                >
                  <th scope="row">{{ index + 1 }}</th>
                  <td>
                    <img
                      :src="'../assets/image/' + keranjang.products.gambar"
                      class="img-fluid shadow"
                      alt="..."
                      width="200px"
                    />
                  </td>
                  <td>
                    <strong>{{ keranjang.products.nama }}</strong>
                  </td>
                  <td>{{ keranjang.keterangan }}</td>
                  <td>{{ keranjang.jumlah_pemesanan }}</td>
                  <td align="right">Rp.{{ keranjang.products.harga }},-</td>
                  <td align="right">
                    Rp.{{
                      keranjang.products.harga * keranjang.jumlah_pemesanan
                    }},-
                  </td>
                  <td align="center" class="text-danger">
                    <b-icon-trash
                      @click="hapusKeranjang(keranjang.id)"
                    ></b-icon-trash>
                  </td>
                </tr>
                <tr>
                  <td colspan="6" align="right">
                    <strong>Total harga :</strong>
                  </td>
                  <td>
                    <strong>Rp. {{ totalHarga }}</strong>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
      <!-- form cekout -->
      <div class="row justify-content-end">
        <div class="col-md-4">
          <form v-on:submit.prevent>
            <div class="form-group">
              <label for="">Nama</label>
              <input
                type="text"
                name=""
                id=""
                class="form-control"
                v-model="pesan.nama"
              />
            </div>
            <div class="form-group">
              <label for="">Nomor Meja :</label>
              <input
                type="text"
                name=""
                id=""
                class="form-control"
                v-model="pesan.nomeja"
              />
            </div>
            <button
              type="submit"
              class="btn btn-success float-right"
              @click="checkout"
            >
              <b-icon-cart></b-icon-cart> Checkout
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
// untuk import file
import Navbar from "@/components/Navbar.vue";

export default {
  name: "Keranjang",
  components: {
    Navbar,
  },
  data() {
    return {
      keranjangs: [],
      pesan: [],
    };
  },

  methods: {
    setKeranjang(data) {
      this.keranjangs = data;
    },
    checkout() {
      if (this.pesan.nama && this.pesan.nomeja) {
        this.pesan.keranjangs = this.keranjangs;
        return axios
          .post("http://localhost:3000/pesanans", this.pesan)
          .then(() => {
            this.$router.push({ path: "/pesanan-sukses" });
            this.$toast.success("Sukses Dipesan", {
              type: "success",
              position: "top-right",
              duration: 3000,
              dismissible: true,
            });
          })
          .catch((err) => console.log(err));
      } else {
        this.$toast.error("Nama dan Nomor Meja harap diisi", {
          type: "error",
          position: "top",
          duration: 3000,
          dismissible: true,
        });
      }
    },
    hapusKeranjang(id) {
      axios
        .delete("http://localhost:3000/keranjangs/" + id)
        // handle success
        //  set data json
        .then(() => {
          this.$toast.error("Data Terhapus", {
            type: "error",
            position: "top-right",
            duration: 3000,
            dismissible: true,
          });

          //reload
          axios
            .get("http://localhost:3000/keranjangs")
            // handle success
            //  set data json
            .then((response) => this.setKeranjang(response.data))
            .catch(function (error) {
              // handle error
              console.log(error);
            });
        })
        .catch(function (error) {
          // handle error
          console.log(error);
        });
    },
  },

  mounted() {
    axios
      .get("http://localhost:3000/keranjangs")
      // handle success
      //  set data json
      .then((response) => this.setKeranjang(response.data))
      .catch(function (error) {
        // handle error
        console.log(error);
      });
  },
  computed: {
    totalHarga() {
      return this.keranjangs.reduce(function (items, data) {
        return items + data.products.harga * data.jumlah_pemesanan;
      }, 0);
    },
  },
};
</script>

<style>
</style>
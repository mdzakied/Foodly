<template>
  <div class="food-detail">
    <Navbar />
    <div class="container">
      <!-- Breadcrumb -->
      <div class="row mt-4">
        <div class="col">
          <nav aria-label="breadcrumb">
            <ol class="breadcrumb">
              <li class="breadcrumb-item">
                <router-link to="/" class="text-light">Home</router-link>
              </li>
              <li class="breadcrumb-item">
                <router-link to="/foods" class="text-light">Foods</router-link>
              </li>
              <li class="breadcrumb-item active" aria-current="page">
                Food Order
              </li>
            </ol>
          </nav>
        </div>
      </div>

      <div class="row mt-5">
        <div class="col-md-6 mb-3">
          <b-img
            :src="'../assets/images/' + product.gambar"
            class="img-fluid p-1"
            width="380px"
            center
          />
        </div>
        <div class="col-md-6">
          <h3>
            <strong>{{ product.nama }}</strong>
          </h3>
          <hr />
          <h5>
            Price :
            <strong>Rp. {{ product.harga | numFormat("0,0") }}</strong>
          </h5>
          <form class="mt-4" v-on:submit.prevent>
            <div class="form-group">
              <label for="jumlah_pemesanan">Item Order</label>
              <div class="row mt-2">
                <div class="col-2 col-lg-1 text-center p-0 ml-3">
                  <button
                    class="btn btn-danger"
                    v-on:click="pesan.jumlah_pemesanan -= 1"
                    :disabled="pesan.jumlah_pemesanan <= 1 ? '' : disabled"
                  >
                    -
                  </button>
                </div>
                <div class="col-2 p-0">
                  <input
                    type="number"
                    class="form-control form-jumlah text-center text-light p-0"
                    v-model="pesan.jumlah_pemesanan"
                    style="background-color: transparent; border: none"
                  />
                </div>
                <div class="col-2 col-lg-1 text-center p-0">
                  <button
                    class="btn btn-danger"
                    v-on:click="pesan.jumlah_pemesanan += 1"
                  >
                    +
                  </button>
                </div>
                <div class="col-9"></div>
              </div>
            </div>
            <div class="form-group">
              <label for="keterangan"> Description</label>
              <textarea
                v-model="pesan.keterangan"
                class="form-control"
                placeholder="Desc : Spicy, Extra Salt ..."
              ></textarea>
            </div>

            <button type="submit" class="btn btn-success" @click="pemesanan">
              Order
            </button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import axios from "axios";

export default {
  name: "FoodDetail",
  components: {
    Navbar,
  },
  data() {
    return {
      product: {},
      pesan: {
        jumlah_pemesanan: 1,
      },
    };
  },
  methods: {
    setProduct(data) {
      this.product = data;
    },
    pemesanan() {
      if (this.pesan.jumlah_pemesanan) {
        this.pesan.products = this.product;
        axios
          .post("http://localhost:3000/keranjangs", this.pesan)
          .then(() => {
            this.$router.push({ path: "/keranjang" });
            this.$swal.fire({
              icon: "success",
              title: "Success",
              text: "Your food add to cart",
              showConfirmButton: false,
              timer: 1500,
            });
          })
          .catch((err) => console.log(err));
      } else {
        this.$swal.fire({
          icon: "error",
          title: "Oops...",
          text: "Something went wrong!",
          showConfirmButton: false,
          timer: 1500,
        });
      }
    },
  },
  mounted() {
    axios
      .get("http://localhost:3000/products/" + this.$route.params.id)
      .then((response) => this.setProduct(response.data))
      .catch((error) => console.log(error));
  },
};
</script>
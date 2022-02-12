<template>
  <div>
    <div class="container">
      <div class="row mt-4">
        <div class="col">
          <h2>
            <strong>Food</strong>
            List
          </h2>
        </div>
      </div>
      <div class="row mt-3">
        <div class="col">
          <div class="input-group mb-3">
            <input
              v-model="search"
              type="text"
              class="form-control text-light search-bar-hero"
              placeholder="Masak Apa Hari Ini ? ..."
              aria-label="Cari"
              aria-describedby="basic-addon1"
              @keyup="searchFood"
            />
            <div class="input-group-prepend">
              <span
                class="input-group-text search-bar-icon"
                id="basic-addon1"
                style="cursor: pointer"
              >
                <b-icon-search variant="light"></b-icon-search>
              </span>
            </div>
          </div>
        </div>
      </div>

      <div class="row mb-4">
        <!-- Empety Search -->
        <div class="col-12 text-center mt-4 p-2" v-if="!products.length">
          <img
            src="../assets/images/empty-search.png"
            alt="image empty food"
            style="max-width: 300px"
          />
          <h2 class="mt-4"><strong>Sory :(</strong></h2>
          <h4>
            Food Not Yet Available <br />
            Please Choose Other Food
          </h4>
        </div>

        <!-- Search -->
        <div
          class="col-md-4 mt-4"
          v-for="product in products"
          :key="product.id"
        >
          <CardProduct :product="product" />

          <div class="card text-dark" style="max-width: 20rem">
            <img
              class="card-img-top"
              src="https://placekitten.com/300/300"
              alt="Card image cap"
            />
            <img
              class="card-img-top"
              src="../assets/images/foodly.png"
              alt="Card image cap"
            />
            <div class="card-body">
              <h5 class="card-title">Card title</h5>
              <p class="card-text">
                Some quick example text to build on the card title and make up
                the bulk of the card's content.
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import CardProduct from "@/components/CardProduct.vue";
import axios from "axios";

export default {
  name: "Foods",
  components: {
    CardProduct,
  },
  data() {
    return {
      products: [],
      search: "",
    };
  },
  created() {
    this.search = this.$route.params.data;
  },
  methods: {
    setResults(data) {
      this.results = data;
    },
    searchFood() {
      axios
        .get("http://localhost:3000/products?q=" + this.search)
        .then((response) => this.setProducts(response.data))
        .catch((error) => console.log(error));
    },
  },
  mounted() {
    window.scrollTo(0, 0);
    axios
      .get("https://quran-endpoint.vercel.app/")
      .then((response) => {
        this.setResults(response.data);
        console.log(response.data);
      })
      .catch((error) => console.log(error));
    if (this.search.length) {
      axios
        .get("http://localhost:3000/products?q=" + this.search)
        .then((response) => this.setProducts(response.data))
        .catch((error) => console.log(error));
    }
  },
};
</script>

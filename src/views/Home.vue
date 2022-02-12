<template>
  <div class="home">
    <div class="container">
      <!-- Desktop -->
      <div class="d-none d-md-block">
        <div class="row mt-5">
          <div class="col-md-5">
            <div class="hero-content-bg">MAKAN</div>
            <div class="hero-content">
              <h1>
                <strong>
                  Resep Menu<br />
                  Makanan Indonesia
                </strong>
              </h1>
              <div class="input-group mt-4">
                <input
                  v-model="search"
                  type="text"
                  class="form-control text-light search-bar-hero"
                  placeholder="Masak Apa Hari Ini ? ..."
                  aria-label="Cari"
                  aria-describedby="basic-addon1"
                />

                <div class="input-group-prepend">
                  <span
                    class="input-group-text search-bar-icon"
                    id="basic-addon1"
                    style="cursor: pointer"
                    @click="searchFood"
                  >
                    <b-icon-arrow-right variant="light"></b-icon-arrow-right>
                  </span>
                </div>
              </div>
            </div>
          </div>
          <div class="col-md-7 mt-1">
            <img
              src="../assets/images/hero.png"
              alt="image hero"
              class="hero-img"
            />
          </div>
        </div>
      </div>

      <!-- Mobile -->
      <div class="d-sm-block d-md-none">
        <div class="row hero-img-bg">
          <div class="col-md-6 mb-3"></div>
          <div class="col-md-6">
            <div class="hero-content-bg-mb">MAKAN</div>
            <div class="hero-content-mb">
              <h1 class="margin-mb">
                <strong>
                  Resep Menu<br />
                  Makanan Indonesia
                </strong>
              </h1>
              <div class="input-group">
                <input
                  v-model="search"
                  type="text"
                  class="form-control text-light search-bar-hero"
                  placeholder="Masak Apa Hari Ini ? ..."
                  aria-label="Cari"
                  aria-describedby="basic-addon1"
                  @keyup.enter="searchFood"
                />
                <div class="input-group-prepend">
                  <span
                    class="input-group-text search-bar-icon"
                    id="basic-addon1"
                    style="cursor: pointer"
                    @click="searchFood"
                  >
                    <b-icon-arrow-right variant="light"></b-icon-arrow-right>
                  </span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  data() {
    return {
      search: "",
    };
  },
  methods: {
    searchFood() {
      this.$router.push({ name: "Foods", params: { data: this.search } });
    },
  },
};
</script>
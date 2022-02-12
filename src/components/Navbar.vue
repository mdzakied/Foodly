<template>
  <div>
    <b-navbar id="navbar" toggleable="lg" type="dark" class="border-none">
      <div class="container mt-4">
        <b-navbar-brand class="m-0">
          <router-link to="/">
            <img src="../assets/images/foodly.png" width="100px" />
          </router-link>
        </b-navbar-brand>

        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

        <b-collapse id="nav-collapse" is-nav>
          <b-navbar-nav class="ml-auto">
            <li class="nav-item">
              <router-link class="nav-link text-light" to="/">Home</router-link>
            </li>
            <li class="nav-item">
              <router-link class="nav-link text-light" to="/foods"
                >Menu Makanan</router-link
              >
            </li>
          </b-navbar-nav>

          <!-- Right aligned nav items -->
          <b-navbar-nav class="ml-auto">
            <li class="nav-item">
              <router-link
                class="nav-link text-light border border-light pl-3 pr-3"
                to="/keranjang"
              >
                Favorite
                <b-icon-heart-fill
                  font-scale="0.9"
                  shift-h="2"
                  shift-v="3"
                ></b-icon-heart-fill>
              </router-link>
            </li>
          </b-navbar-nav>
        </b-collapse>
      </div>
    </b-navbar>
  </div>
</template>

<script>
export default {
  name: "Navbar",
};
</script>
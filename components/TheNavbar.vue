<template>
  <nav class="navbar navbar-expand-lg navbar-light " style="height: 15vh; margin-top: 10px;">
    <div class="container-fluid">
      <a class="navbar-brand" style="width: 40%;">
        <img src="../public/photo/Logo_horizontal.png" alt="" width="40%" height="auto">
      </a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav"
        aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div v-if="showNav" class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav ms-auto ">
          <li class="nav-item">
            <NuxtLink to="/" style="text-decoration: none  !important;" @click="closeNav"> <a class="nav-link fw-bold h5">Accueil</a>
            </NuxtLink>
          </li>

          <li class="nav-item">
            <NuxtLink to="/apropos" style="text-decoration: none  !important;" @click="closeNav"> <a class="nav-link fw-bold h5">A
                Propos</a></NuxtLink>
          </li>
          <li class="nav-item">
            <a class="nav-link fw-bold h5" style="color:#175c27; text-decoration: none:  !important;" @click="closeNav"
              href="https://www.fiverr.com/bastienville713">Contact</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
export default {
    data() {
        return {
            showNav: true
        };
    },
    methods: {
      dispa() {
      this.$router.push('/');
    },
        closeNav() {
            if (this.showNav == true ) {
                this.showNav = false;
                setTimeout(() => {
        this.showNav = true;
      }, 2);
                
            } else {
              this.showNav = true;
            }
        }
    },
  }
  </script>
<style scoped>


@media only screen and (max-width: 767px) {
  .navbar-collapse {
    box-shadow: 2px 2px 2px 2px rgba(0, 0, 0, 0.575);
  }

  h2 {
    font-size: 2vh !important;
  }

  .navbar {
    text-align: center;
  }

  .nav-item {
    text-align: center;
  }

  .navbar-collapse {
    background-color: white;
    margin-top: -30%;
  }

  button {
    margin-bottom: 30%;
    margin-right: 40%;
  }

  img {
    width: 70%;
    height: auto;
  }


}</style>

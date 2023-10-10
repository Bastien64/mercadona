<template>
  <div class="login">
    <form class="form" @submit.prevent="login">
      <h1>Interface Admin</h1>
      <label for="username">Username</label>
      <input v-model="username" name="username" type="text" class="input" required /><br>
      <label for="password">Password</label>
      <input v-model="password" name="password" type="password" class="input" required /><br>
      <button class="btn btn-danger">Login</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    async login() {
      try {
        const response = await axios.post('https://bastien-353a308d211c.herokuapp.com/admin', {
          login: this.username, // Utilisez this.username ici
          password: this.password
        });

        // Stockez le jeton JWT ou d'autres informations d'authentification dans le local storage
        localStorage.setItem("Admin", this.username);
        console.log (localStorage.getItem("Admin"));
        this.$router.push({ name: "protected" });
      } catch (error) {
        alert("Nom d'utilisateur ou mot de passe incorrect.");
      }
    },
  },
  beforeMount() {
    this.loading = true;
    axios.get('https://bastien-353a308d211c.herokuapp.com/admin/get?login=' + this.username) // Utilisez this.username ici
      .then(response => {
        this.loading = false;
        this.admin = response.data[0];
        console.log(this.admin);
      })
      .catch(error => {
        this.loading = false;
        this.error = `Une erreur s'est produite : ${error.message}`;
      });
  }
}
</script>


<style>
.login {
  text-align: center;
  height: auto;
  border: 2px black;
}

h1 {
  font-weight: bold;
}

label {
  font-weight: bold;
  margin-top: 5%;
  margin-right: 2%;
}

button {
  margin-top: 5%;
}

@media only screen and (max-width: 767px) {
  .login {
    margin-top: 30%;
  }
}</style>
  
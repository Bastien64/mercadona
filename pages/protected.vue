<template>
    <div class="card" >
        <div class="card-body">
            <h1> Bienvenue sur l'interface administrateur </h1>
            <p>Vous pouvez  : ajouter des photos, voir les votes et télécharger la base de données des Votants</p>
            <button class="btn btn-danger" @click="logout">Logout</button>
        </div>
    </div>
    <div class="effet"></div>
<Theprotectedcol/>
</template>
  
<script>
import axios from 'axios';
export default {
    beforeMount() {
        const isAdmin = localStorage.getItem("Admin") === "Admin";
        if (!isAdmin) {
            const router = useRouter();
            router.push({ path: "/" });
        }
    },
    data() {
        return {
            username: window.user,
            Prenom: "",
            Nom: "",
            Image: null,
        };
    },
    methods: {
        logout() {
            window.user = null;
            localStorage.removeItem("Admin");
            const router = useRouter();
            router.push({ path: "/", query: { logout: null } });
        },
    },
};
</script>
  
<style scoped>




@media only screen and (min-width: 768px) {
.photo {
    width: 10%;
    margin: 0 auto;
    /* Added */
    float: none;
    /* Added */
    margin-bottom: 10px;
    /* Added */
    text-align: center;
    max-width: 25%;
}

.card {
    margin: 0 auto;
    /* Added */
    float: none;
    /* Added */
    margin-bottom: 10px;
    /* Added */
    text-align: center;
    max-width: 25%;
    box-shadow: 2px 2px 1px 2px black;
}

.effet {
    margin-top: 5%;
    margin-bottom: 5%;
    margin-left: auto;
    margin-right: auto;
    width: 45%;
    height: 5px;
    background-color: #fa8f0dad
}
}

@media only screen and (max-width: 767px) {
    .card{
width: 90% !important;
margin-top: 25%;
margin-left: auto;
margin-right: auto;

    float: none;

    margin-bottom: 10px;

    text-align: center;
    box-shadow: 2px 2px 1px 2px black;
}
}

</style>
<template>
    <div class="box"> <h1>Participer</h1>
    <p>Nous sommes ravis d'annoncer notre prochain concours photo, qui offrira aux participants la chance de remporter des prix fantastiques ! Pour participer, vous devez tout d'abord vous rendre dans notre studio photo, où vous pourrez prendre une photo sur le thème du concours.</p>
    <div class="effet"></div>
    <p>Ensuite, nous téléchargerons sur notre site web dédié au concours et remplir le formulaire de participation. Assurez-vous de fournir toutes les informations requises, y compris votre nom, votre adresse email et votre numéro de téléphone lors de vôtre visite au studio.</p>
    <div class="effet"></div>
    <p>Les soumissions doivent être reçues avant la date limite du concours, et les gagnants seront annoncés peu de temps après. Alors n'hésitez plus, venez nous voir au studio photo et montrez-nous votre talent pour la photographie ! Nous sommes impatients !</p>

    <button class="btn btn-danger" href="https://www.studioimagein.com/contact/"> Nous contacter</button>
</div>
</template>

<style scoped>

.effet {
    margin-top: 5%;
    margin-bottom: 5%;
    width: 25%;
    height: 5px;
    margin-left: auto;
    margin-right: auto;
    background-color: rgba(250, 143, 13, 0.678)
}
.box{
    width: 60%;
    height: auto;
    box-shadow: 5px 5px 5px rgba(0, 0, 0, 0.322) ;
    margin: auto;
    text-align: center;
    padding: 2%;
    }

    br{
        margin: 5px;
    }
    @media only screen and (max-width: 767px) {
        .box{
    width: 90%;
    height: auto;
    box-shadow: 5px 5px 5px rgba(0, 0, 0, 0.322) ;
    margin-top: 20%;
    margin-right: auto;    margin-left: auto;
    text-align: center;
    padding: 2%;
    }

    br{
        margin: 5px;
    }

    .effet {
    margin-top: 10%;
    margin-bottom: 10%;
    margin-left: auto;
    margin-right: auto;
    width: 25%;
    height: 5px;
    background-color: #fa8f0dad
}
}
    
</style>
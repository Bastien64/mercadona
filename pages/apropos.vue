<template>
    <div class="box"> <h1>About us</h1>
    <p>Mercadona, a family company, is one of the leading physical supermarket and online shopping companies in Spain. Its goal is to be responsible for prescribing “The Boss” (customer) the best option to satisfy its food, home care, personal care and animal care. Thanks to this, 5.7 million households place their trust in the company every day. </p>
    <div class="effet"></div>
    <p>Created in 1977 by the Cárnicas Roig Group, currently it has 1.627 stores across Spain and 42 in Portugal, and a staff of 99.000 employees who seek excellence, 3.500 of them in Portugal.</p>
    <div class="effet"></div>
    <p>“Achieving a Sustainable Agri-Food Chain, which people want to exist and feel proud of, led by Mercadona, and with ‘The Boss’ as its lighthouse”.</p>
    <div class="effet"></div>
</div>
</template>

<style scoped>
.box{
    width: 60%;
    height: auto;
    box-shadow: 5px 5px 5px rgba(0, 0, 0, 0.322) ;
   margin: auto;
    text-align: center;
    padding: 2%;
    }

    .effet {
    margin-top: 5%;
    margin-bottom: 5%;
    width: 25%;
    height: 5px;
    margin-left: auto;
    margin-right: auto;
    background-color: rgba(250, 143, 13, 0.678)
}

    br{
        margin: 5px;
    }
    @media only screen and (max-width: 767px) {
        .box{
    width: 90%;
    height: auto;
    box-shadow: 5px 5px 5px rgba(0, 0, 0, 0.322) ;
    margin-top: 20% ;
    margin-left: auto;
    margin-right: auto;
    text-align: center;
    padding: 5%;
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
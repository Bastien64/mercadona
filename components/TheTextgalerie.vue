<template>
    <div class="card-body">
        <h3>Galerie Photos</h3>
        <p>Le concours s'adresse à tous les passionnés de photographie, amateurs ou professionnels. À la fin du concours,  le photographe avec la photo qui accumule plus grand nombre de vote se verra décerner un prix </p>
    </div>
</template>


<style scoped>
div {
    width: 60%;
    height: auto;
    box-shadow: 5px 5px 5px rgba(0, 0, 0, 0.322) ;
}

div:hover {
    transition: 0.5s;   
    width: 60%;
    height: auto;
    box-shadow:  hsla(33, 96%, 52%, 0.4) 0.5px 5px 5px, rgba(250, 143, 13, 0.3) 10px 10px,  rgba(250, 143, 13, 0.2) 15px 15px,  rgba(250, 143, 13, 0.1) 20px 20px,  rgba(250, 143, 13, 0.05) 25px 25px;
}

h3{
    padding-top: 2vh;
    font-weight: bold;
    text-align: center;
}
p{
    text-align: center;
    padding-bottom: 5vh;
}

@media screen {
    
}
</style>
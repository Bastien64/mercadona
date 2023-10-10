<template>
    <div class="text"><TheTextgalerie /></div>
    <div class="effet"></div>
    <div class="photo"><ThePhoto /></div>
    <div class="cookies"><TheCookies /></div>
    <div class="effet"></div>
      
</template>

<style scoped>

div {
    margin: auto;
    margin-top: 2vh;
}
.effet {
    margin-top: 5%;
    margin-bottom: 5%;
    width: 25%;
    height: 5px;
    background-color: rgba(250, 143, 13, 0.678)
}
.photo {
    margin-top: 5vh;
    margin-left: 5%;
}

.cookies {
    border-radius: 10%;

}

@media only screen and (max-width: 767px) {
    .text {
        margin-top: 20%;
    }
    .photo{
    max-width: 100vw;
}
.effet {
    margin-top: 10%;
    margin-bottom: 10%;
    width: 25%;
    height: 5px;
    background-color: #fa8f0dad
}
}

</style>
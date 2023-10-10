<template>
    <div class="black">
        <img src="../public/photo/banniere.jpeg" alt="">
    </div>
</template>

<style scoped>
@media only screen and (min-width: 990px) {
    .black {
        margin-top: 2%;
        width: 100%;
        height: 45vh;
        background-color: black;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    img{
        margin-top: 2%;
        text-align: center;
    width: 80vw;
    height: 40vh;
}
}

@media only screen and (max-width: 989px) {
    img{
    width: 100vw;
    margin-top: 10%;
}
}


@media only screen and (max-width: 767px) {
    img{
    width: 0vw;
    margin-top: 15%;
}
}

</style>
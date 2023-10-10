<template>
    <div v-if="showPopup" class="container">
        <div class="cookiesContent" id="cookiesPopup">
            <button class="close" @click="closePopup">✖</button>
            <img src="https://cdn-icons-png.flaticon.com/512/1047/1047711.png" alt="cookies-img" />
            <p>Nous utilisons des cookies a des fins statistiques, marketing et publicitaires.</p>
            <button class="accept" @click="closePopup">C'est Ok !</button>
            <a href="https://google.com" style=""><button class="denied" @click="closePopup" >Retour sur Google !</button> </a>
        </div>
    </div>
</template>

<script>
import Cookies from 'js-cookie';
export default {
    data() {
        return {
            showPopup: true
        };
    },
    methods: {
        closePopup() {
            if (!Cookies.get('showPopup')) {
                Cookies.set('showPopup', 'true', { expires: 40 });
                this.showPopup = false;
            } else {
                this.showPopup = false;
            }
        }
    },
    created() {
        if (Cookies.get('showPopup')) {
            this.showPopup = false;
        }
    },
};
</script>

<style scoped>
.cookiesContent {
    width: 25%;
    padding: 2%;
    box-shadow: 2px 2px 2px 2px rgba(0, 0, 0, 0.329);
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 999;
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: #fff;
    color: #000;
    text-align: center;
    border-radius: 20px;
    padding: 30px 30px 70px;
}

.cookiesContent button.close {
    width: 30px;
    font-size: 20px;
    color: #c0c5cb;
    align-self: flex-end;
    background-color: transparent;
    border: none;
    margin-bottom: 10px;
}

.cookiesContent img {
    width: 82px;
    margin-bottom: 15px;
}

.cookiesContent p {
    margin-bottom: 40px;
    font-size: 18px;
}

.cookiesContent button.accept {
    background-color: #ed6755;
    border: none;
    border-radius: 5px;
    width: 200px;
    padding: 14px;
    font-size: 16px;
    color: white;
    box-shadow: 0px 6px 18px -5px #ed6755;
}

.cookiesContent button.denied {
    margin-top: 5%;
    background-color: #000000;
    border: none;
    border-radius: 5px;
    width: 150px;
    padding: 14px;
    font-size: 12px;
    color: white;
    box-shadow: 0px 6px 18px -5px #000000;
} 

@media only screen and (max-width: 767px) {
    .cookiesContent {
    width: 90%;
    padding: 2%;
    box-shadow: 2px 2px 2px 2px rgba(0, 0, 0, 0.329);
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    z-index: 999;
    display: flex;
    flex-direction: column;
    align-items: center;
    background-color: #fff;
    color: #000;
    text-align: center;
    border-radius: 20px;
    padding: 30px 30px 70px;
}
}
</style>
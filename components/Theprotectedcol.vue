<template>
    <div class="produitlist">
        <p>
            <a class="btn btn-primary" data-bs-toggle="collapse" href="#produit" role="button" aria-expanded="false"
                aria-controls="produit">
                Les produits
            </a>
        </p>
        <div class="collapse" id="produit">
            <div class="card card-body">
                <div v-for="produit in produits">
                    <div class="card " style="width: 18rem; margin-left: 10px; ">
                        <img :src="produit.image" class="card-img-top" alt="...">
                        <div class="card-body">
                            <h5 class="card-title">{{ produit.description }}</h5>
                            <p :class="{ 'discounted-price-style': hasDiscount(produit.id) }">
                    {{ getProductPrice(produit.id) }} €
                </p>
                            <button @click="openPromotionModal(produit)">Ajouter une promotion</button>
                        </div>
                    </div>
                </div>
            </div>
            <div v-if="isPromotionModalOpen">
    <h3>Ajouter une promotion pour {{ selectedProductForPromotion }}</h3>
    <form @submit.prevent="addPromotion">
        <label for="datedebut">Date de début :</label>
        <input type="date" v-model="promotionFormData.datedebut" required>

        <label for="datefin">Date de fin :</label>
        <input type="date" v-model="promotionFormData.datefin" required>

        <label for="pourcentage">Pourcentage de réduction :</label>
        <input type="number" v-model="promotionFormData.pourcentage" required>

        <button type="submit">Ajouter la promotion</button>
    </form>
</div>
        </div>
        <div>
            <h3>Ajouter un nouveau produit :</h3>
            <form @submit.prevent="addProduit">
                <div class="mb-3">
                    <label for="description" class="form-label">Description</label>
                    <input type="text" class="form-control" v-model="newProduit.description" required>
                </div>
                <div class="mb-3">
                    <label for="price" class="form-label">Prix</label>
                    <input type="number" class="form-control" v-model="newProduit.price" required>
                </div>
                <div class="mb-3">
                    <label for="image" class="form-label">Image (base64)</label>
                    <input type="file" class="form-control-file" @change="handleFileChange" accept="image/*">
                    <img :src="selectedImage" v-if="selectedImage" alt="Aperçu de l'image" class="mt-2 img-thumbnail"
                        style="max-width: 200px;">
                </div>
                <div class="mb-3">
                    <label for="categorie_id" class="form-label" style="color: black!important;">Catégorie</label>
                    <select class="form-select" v-model="newProduit.categorie_id" required style="color: black!important;">
                        <option value="" disabled>Choisissez une catégorie</option>
                        <option v-for="category in categories" :value="category.id">{{ category.libelle
                        }}</option>
                    </select>
                </div>
                <button type="submit" class="btn btn-primary">Ajouter</button>
            </form>
        </div>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            produits: [],
            loading: true,
            categories: [],
            selectedCategoryId: null,
            promotions: [],
            newProduit: {
                description: '',
                price: '',
                image: '',
                categorie_id: '',
            },
            selectedImage: null,
            isPromotionModalOpen: false,
        selectedProductForPromotion: null,
        promotionFormData: {
            datedebut: '',
            datefin: '',
            pourcentage: '',
        },
        };
    },
    methods: {
        hasDiscount(produitId) {
        const promotion = this.promotions.find(promotion => promotion.produit_id === produitId);
        return promotion !== undefined;
    },
    getProductPrice(produitId) {
        const produit = this.produits.find(produit => produit.id === produitId);
        if (!produit) {
            return 0;
        }
        const promotion = this.promotions.find(promotion => promotion.produit_id === produitId);
        if (promotion) {
            const discountPercentage = promotion.pourcentage / 100;
            const discountedPrice = produit.price * (1 - discountPercentage);
            return discountedPrice < 0 ? 0 : discountedPrice;
        } else {
            return produit.price;
        }
    },
        openPromotionModal(produit) {
        // Initialisez les champs du formulaire de promotion
        this.selectedProductForPromotion = produit.id; // Assurez-vous que vous avez un identifiant unique pour chaque produit
        this.promotionFormData = {
            datedebut: '',
            datefin: '',
            pourcentage: '',
        };
        this.isPromotionModalOpen = true; // Activez la fenêtre modale de promotion
    },
    addPromotion() {
        const promotionData = {
            datedebut: this.promotionFormData.datedebut,
            datefin: this.promotionFormData.datefin,
            pourcentage: this.promotionFormData.pourcentage,
            produit_id: this.selectedProductForPromotion,
        };

        axios.post('https://bastien-353a308d211c.herokuapp.com/promotion', promotionData)
            .then(response => {
                // Réinitialisez les données du formulaire et fermez la fenêtre modale
                this.promotionFormData = {
                    datedebut: '',
                    datefin: '',
                    pourcentage: '',
                };
                this.isPromotionModalOpen = false;
                console.log('Promotion ajoutée avec succès:', response.data);
            })
            .catch(error => {
                console.error('Erreur lors de l\'ajout de la promotion :', error);
            });
    },
        addProduit() {
            axios
                .post('https://bastien-353a308d211c.herokuapp.com/produit', this.newProduit)
                .then(response => {
                    this.newProduit = {
                        description: '',
                        price: '',
                        image: '',
                        categorie_id: '',
                    };
                    console.log('Produit ajouté avec succès:', response.data);
                })
                .catch(error => {
                    console.error('Erreur lors de l\'ajout du produit :', error);
                });
        },
        loadCategories() {
            axios.get('https://bastien-353a308d211c.herokuapp.com/categorie')
                .then(response => {
                    this.categories = response.data;
                })
                .catch(error => {
                    console.error('Erreur lors du chargement des catégories :', error);
                });
        },

        loadProduits() {
            axios.get('https://bastien-353a308d211c.herokuapp.com/produit')
                .then(response => {
                    this.loading = false;
                    this.produits = response.data;
                    const expirationTime = Date.now() + 10 * 60 * 1000;
                    localStorage.setItem('cachedproduits', JSON.stringify(response.data));
                    localStorage.setItem('cacheExpiration', expirationTime.toString());
                })
                .catch(error => {
                    console.error('Erreur lors du chargement des produits :', error);
                });
        },
        handleFileChange(event) {
            const selectedFile = event.target.files[0];
            if (selectedFile) {
                // Lisez le fichier sélectionné en tant que Data URL (base64)
                const reader = new FileReader();
                reader.onload = () => {
                    this.newProduit.image = reader.result; // Stockez l'image en base64 dans votre modèle
                    this.selectedImage = reader.result; // Affichez l'image sélectionnée
                };
                reader.readAsDataURL(selectedFile);
            }
        },

    },
    mounted() {
        this.loadCategories();
        axios.get('https://bastien-353a308d211c.herokuapp.com/promotion')
            .then(response => {
                this.loading = false;
                this.promotions = response.data;
                console.log('Promotions:', this.promotions);
            })
            .catch(error => {
                console.error('Error:', error);
            });
            axios.get('https://bastien-353a308d211c.herokuapp.com/produit')
                .then(response => {
                    this.loading = false;
                    this.produits = response.data;

                })
                .catch(error => {
                    console.error('Error:', error);
                });
        }
    }
</script> 

<style>
@media only screen and (min-width: 767px) {
.card {
    border: none !important;
    display: flex;
    flex-direction: row;

}

.produitlist {
    display: flex;
    flex-direction: column;
    align-items: center;
    max-height: auto;

}
.discounted-price-style {
    font-weight: bold;
    color: red;
    font-size: 25px;
  }}
@media only screen and (max-width: 767px) {
    .card {
    border: none !important;
    margin-left: 10px;
    margin-top: 10px;
    width: auto;
  }

  img {
    float: left;
    width: 100px;
    height: auto;
    object-fit: cover;
  }
.produitlist {
    display: flex;
    flex-direction: column;
    align-items: center;
    max-height: auto;

}
.discounted-price-style {
    font-weight: bold;
    color: red;
    font-size: 25px;
  }
}
</style>
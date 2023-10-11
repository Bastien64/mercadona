<template>
  <div>
    <div v-if="loading" class="loading-animation" style="display: flex; flex-direction: column;">
      <p style="font-weight: bold;">En chargement ...</p>
    </div>
    <div v-else class="categorie">
      <div style="display: flex; flex-direction: row;">
        <div v-for="categorie in categories" :key="categorie.id" class="col-md-3 mb-3 ">
          <button type="button" class="btn btn-success" @click="filterByCategory(categorie.id)">{{ categorie.libelle
          }}</button>
        </div>
      </div>
      <div class="row row-cols-1 row-cols-md-3 g-4">
        <div v-for="produit in filteredProduits" :key="produit.id" class="col-md-4 mb-2">
          <div class="card h-100 w-75 align-items-center justify-content-center">
            <img :src="produit.image" class="card-img-top" alt="...">
            <div class="card-body">
              <h5 class="card-title">{{ produit.description }}</h5>
              <p :class="{ 'discounted-price-style': hasDiscount(produit.id) }">
                {{ getProductPrice(produit.id) }} €
              </p>


              <p class="badge bg-success">{{ getCategoryLabel(produit.categorie_id) }}</p>
            </div>
          </div>
        </div>
      </div>
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

    }
  },
  computed: {
    filteredProduits() {
      if (this.selectedCategoryId === null) {
        return this.produits;
      } else {
        return this.produits.filter(produit => produit.categorie_id === this.selectedCategoryId);
      }
    }
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
    calculateDiscountedPrice(produit) {
      const promotion = this.promotions.find(promotion => promotion.produit_id === produit.id);
      if (promotion) {
        console.log('Found promotion for product', produit.id, 'with percentage', promotion.pourcentage);
        const discountPercentage = promotion.pourcentage / 100;
        const discountedPrice = produit.price * (1 - discountPercentage);
        if (discountedPrice < 0) {
          return 0;
        }
        console.log('Discounted price:', discountedPrice);
        return discountedPrice;
      } else {
        console.log('No promotion found for product', produit.id);
        return produit.price;
      }
    },
    getCategoryLabel(categorieId) {
      const category = this.categories.find(category => category.id === categorieId);
      return category ? category.libelle : 'Catégorie inconnue';
    },
    filterByCategory(categoryId) {
      this.selectedCategoryId = categoryId;
    }
  },
  mounted() {
    axios.get('https://bastien-353a308d211c.herokuapp.com/categorie')
      .then(response => {
        this.loading = false;
        this.categories = response.data;
      })
      .catch(error => {
        console.error('Error:', error);
      });
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
        this.produits = response.data; // Mettez à jour la liste des produits
      })
      .catch(error => {
        console.error('Error:', error);
      });
  }
}
</script>

<style scoped>
@media only screen and (min-width: 767px) {
  .card {
    border: none !important;
    margin-left: 10px;
    margin-top: 10px;

  }

  img {
    opacity: 0.9;
    width: 200px;
    height: 200px;
    object-fit: cover;
  }

  .discounted-price-style {
    font-weight: bold;
    color: red;
    font-size: 25px;
  }

}



@media only screen and (max-width: 767px) {
  .card {
    border: none !important;
    margin-left: 10px;
    margin-top: 10px;
    width: auto;
  }

  img {
    float: left;
    width: 50%;
    height: auto;
    object-fit: cover;
  }

  .discounted-price-style {
    font-weight: bold;
    color: red;
    font-size: 25px;
  }

  .categorie {
    display: flex;
    flex-direction: column;
  }
}
</style>
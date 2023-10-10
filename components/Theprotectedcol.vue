<template>
    <div class="collaps">
        <div>
            <p class="pleft">
                <button class="btn btn-danger" type="button" data-bs-toggle="collapse" data-bs-target="#Ajouterphoto"
                    aria-expanded="false" aria-controls="Ajouterphoto">
                    Ajouter des photos
                </button>
            </p>
            <div style="min-height: 120px; ">
                <div class="collapse collapse-horizontal" id="Ajouterphoto">
                    <div class="card card-body" style="width: 50%;">
                        <div class="photo">
                            <form @submit.prevent="updateData">
                                <label>Prénom :</label>
                                <input type="text" v-model="Prenom" /> <br>
                                <label>Nom :</label>
                                <input type="text" v-model="Nom" /><br>
                                <label for="FormControlFile">Photo:</label>
                                <input type="file" class="form-control-file" id="FormControlFile"
                                    @change="onFileChange" /><br>
                                <button type="submit" class="m-3 btn btn-success">Mettre à jour</button>
                                <p>Les données seront à jour après 10 minutes sur l'interface client.</p>
                            </form>
                            <p>{{ updateMessage }}</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div style="max-height: 25% !important;">
            <p class="pleft">
                <button class="btn btn-danger disable" type="button" data-bs-toggle="collapse"
                    data-bs-target="#VoirlesVotes" aria-expanded="false" aria-controls="VoirlesVotes" disabled>
                    Les votes
                </button>
            </p>
            <div>
                <div class="collapse collapse-horizontal" id="VoirlesVotes" style="display: flex; ">
                    <div v-for="photo in photos" style="margin-left: 2px;">
                        <img style="width: 100%;" :src="getPhotoURL(photo.Link)">
                        <p> {{ photo.Nom }} {{ photo.Vote }}</p>
                        <button class="btn btn-secondary" @click="deletePhoto(photo.id)">Supprimer</button>
                    </div>
                </div>
            </div>
        </div>
        <div>
    <button  class="btn btn-danger disable"  @click="downloadCsv">Télécharger base de données des Votants</button>
  </div>
    </div>
</template>


<script>

import axios from 'axios';
export default {
    data() {
        return {
            Prenom: "",
            Nom: "",
            Image: null,
            photos: [],
            updateMessage: "", // Ajout de la variable pour le message de mise à jour
        };
    },
    mounted() {
        axios.get('https://www.studioimageflask.com/photo')
            .then(response => {
                this.loading = false;
                this.photos = response.data;
                console.log(this.photos)
            })
            .catch(error => {
                console.error('Error:', error);
            });

    },
    methods: {
        deletePhoto(photoId) {
            axios.delete(`https://www.studioimageflask.com/photo/delete/${photoId}`)

            .then(response => {
                const index = this.photos.findIndex(photo => photo.id === photoId);
                if (index !== -1) {
                    this.photos.splice(index, 1);
                }
                alert("La photo a été supprimée avec succès");
            })
            .catch(error => {
                console.error(error);
                alert("Une erreur s'est produite lors de la suppression de la photo");
            });
    },
        getPhotoURL(base64Data) {
            const binaryData = atob(base64Data);
            const mimeType = 'image/jpeg'; // à adapter en fonction du type de données
            const arrayBuffer = new ArrayBuffer(binaryData.length);
            const uint8Array = new Uint8Array(arrayBuffer);
            for (let i = 0; i < binaryData.length; i++) {
                uint8Array[i] = binaryData.charCodeAt(i);
            }
            const blob = new Blob([arrayBuffer], { type: mimeType });
            const urlCreator = window.URL || window.webkitURL;
            const imageUrl = urlCreator.createObjectURL(blob);
            return imageUrl;
        },
        onFileChange(event) {
            // Créer un objet FormData et ajouter le fichier sélectionné
            const file = event.target.files[0];
            const formData = new FormData();
            formData.append("Image", file);
            this.Image = formData;
        },
        downloadCsv() {
            axios.get('https://www.studioimageflask.com/download', { responseType: 'blob' })
                .then(response => {
                    const url = window.URL.createObjectURL(new Blob([response.data]))
                    const link = document.createElement('a')
                    link.href = url
                    link.setAttribute('download', 'admins.csv')
                    document.body.appendChild(link)
                    link.click()
                })
        },
        updateData() {
            const formData = new FormData();
            formData.append('Prenom', this.Prenom);
            formData.append('Nom', this.Nom);
            formData.append('Image', this.Image.get('Image'));
            axios.post("https://www.studioimageflask.com/photo", formData, {
                headers: {
                    "Content-Type": "multipart/form-data"
                }
            })
                .then(response => {
                    console.log(response.data);
                    const newPhoto = response.data;
                    newPhoto.imageUrl = this.getPhotoURL(newPhoto.Link);
                    this.photos.push(newPhoto);
                    alert("Merci de votre participation");
                })
                .catch(error => {
                    console.error(error);
                });
                this.updateMessage = "Donnée mise à jour"; // Ajout du message de mise à jour
                setTimeout(() => {
            location.reload();
        }, 1000);
        }
    },
};
</script>

<style>
.collaps {
    display: flex;
    flex-direction: column;
    ;
    width: 70%;
    margin-left: auto;
    margin-right: auto;
}

.pleft {
    margin-left: 5px;
}</style>
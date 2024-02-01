<template>
    <v-container>
        <v-data-iterator :items="this.prodotti" :items-per-page="itemsPerPage">
            <template v-slot:header="{ page, pageCount, prevPage, nextPage }">
                <h1 class="text-h4 font-weight-bold d-flex justify-space-between mb-4 align-center">
                    <div class="text-truncate">
                        Prodotti totali: {{ prodotti.length }}
                    </div>

                    <div class="d-flex align-center">
                        <v-btn class="me-8" variant="text" @click="onClickSeeAll()">
                            <span class="text-decoration-underline text-none">See all</span>
                        </v-btn>

                        <div class="d-inline-flex">
                            <v-btn :disabled="page === 1" icon="mdi-arrow-left" size="small" variant="tonal" class="me-2"
                                @click="prevPage"></v-btn>

                            <v-btn :disabled="page === pageCount" icon="mdi-arrow-right" size="small" variant="tonal"
                                @click="nextPage"></v-btn>
                        </div>
                    </div>
                </h1>
            </template>

            <template v-slot:default="{ items }">
                <v-row>
                    <v-col v-for="(item, i) in items" :key="i" cols="12" sm="6" xl="3">
                        <v-sheet border>
                            <v-img :src="item.raw.thumbnail" cover height="150"></v-img>

                            <v-list-item :title="item.raw.title" lines="two" density="comfortable"
                                :subtitle="item.raw.description.substring(0, 50)">
                                <template v-slot:title>
                                    <strong class="text-h6">
                                        {{ item.raw.title }}
                                    </strong>
                                </template>
                            </v-list-item>

                            <v-table density="compact" class="text-caption">
                                <tbody>


                                    <tr align="right">
                                        <th>Voto {{ item.raw.rating }}</th>

                                        <td><v-rating v-model="item.raw.rating" readonly half-increments></v-rating></td>
                                    </tr>

                                    <tr align="right">
                                        <th>Quantità:</th>

                                        <td>{{ item.raw.stock }}</td>
                                    </tr>

                                    <tr align="right">
                                        <th>Categoria:</th>

                                        <td>{{ item.raw.category }}</td>
                                    </tr>

                                    <tr align="right">
                                        <th>Sconto:</th>

                                        <td>{{ item.raw.discountPercentage }} %</td>
                                    </tr>
                                    <tr align="right">
                                        <th>Price:</th>

                                        <td>€ {{ item.raw.price }}</td>
                                    </tr>
                                    <tr align="right">
                                        <td colspan="2">
                                            <v-expansion-panels>
                                                <v-expansion-panel>
                                                    <v-expansion-panel-title>
                                                        <template v-slot:default="{ expanded }">
                                                            <v-row no-gutters>
                                                                <v-col cols="4" class="d-flex justify-start">
                                                                    Galleria
                                                                </v-col>
                                                                <v-col cols="8" class="text-grey">
                                                                    <v-fade-transition leave-absolute>
                                                                        <span v-if="expanded" key="0">
                                                                        </span>
                                                                        <span v-else key="1">

                                                                        </span>
                                                                    </v-fade-transition>
                                                                </v-col>
                                                            </v-row>
                                                        </template>
                                                    </v-expansion-panel-title>
                                                    <v-expansion-panel-text>
                                                        <v-row>
                                                            <v-col>
                                                                <v-carousel hide-delimiters progress="primary">
                                                                    <v-carousel-item v-for="(item, i) in images[i]" :key="i"
                                                                        :src="item" cover
                                                                        style="width:auto;height:auto"></v-carousel-item></v-carousel>
                                                            </v-col>
                                                        </v-row>

                                                        <v-divider></v-divider>

                                                    </v-expansion-panel-text>
                                                </v-expansion-panel>
                                            </v-expansion-panels>
                                        </td>
                                    </tr>
                                    <tr align="right">
                                        <th></th>
                                        <td></td>
                                    </tr>
                                </tbody>
                            </v-table>
                        </v-sheet>
                    </v-col>
                </v-row>
            </template>
        </v-data-iterator>
    </v-container>
</template>

<script>
import prod from '../api/prodotti'
export default {
    name: 'ProdottiView',
    data() {
        return {
            prodotti: [],
            images: [[], []],
            itemsPerPage: 4,
        }
    },
    methods: {
        onClickSeeAll() {
            this.itemsPerPage = this.itemsPerPage === 4 ? this.prodotti.length : 4
        },
        creaArrayImmagini() {
            this.prodotti.forEach((prodotto) => {
                // Inizializza un array per le immagini del prodotto corrente
                const immaginiProdotto = [];

                // Itera attraverso le immagini del prodotto corrente
                prodotto.images.forEach((immagine) => {
                    // Aggiungi l'immagine all'array delle immagini del prodotto corrente
                    immaginiProdotto.push(immagine);
                });

                // Aggiungi l'array delle immagini del prodotto corrente a this.images
                this.images.push(immaginiProdotto);
            });
            //elimina i primi due elementi dell'array
            this.images.splice(0, 2);
        }

    },
    mounted() {
        this.prodotti = prod;
        this.creaArrayImmagini();
    }


    // let i = 0;

    // this.prodotti.forEach(element => {
    //     let j = 0;
    //     element.images.forEach(img => {
    //         this.images[i][j] = img;
    //         j++;
    //     });
    //     i++;
    // });

}



</script>

<template>
    <v-container>
        <v-data-iterator :items="this.prodotti" :items-per-page="itemsPerPage">
            <template v-slot:header="{ page, pageCount, prevPage, nextPage }">
                <h1 class="text-h4 font-weight-bold d-flex justify-space-between mb-4 align-center">
                    <div class="text-truncate">
                        Most popular mice
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
                                :subtitle="item.raw.description">
                                <template v-slot:title>
                                    <strong class="text-h6">
                                        {{ item.raw.title }}
                                    </strong>
                                </template>
                            </v-list-item>

                            <v-table density="compact" class="text-caption">
                                <tbody>
                                    <tr align="right">
                                        <th>Sconto:</th>

                                        <td>{{ item.raw.discountPercentage }} %</td>
                                    </tr>

                                    <tr align="right">
                                        <th>Voto {{item.raw.rating  }}</th>

                                        <td><v-rating v-model="item.raw.rating" readonly half-increments></v-rating></td>
                                    </tr>

                                    <tr align="right">
                                        <th>Weight:</th>

                                        <td>{{ item.raw.rating }}</td>
                                    </tr>

                                    <tr align="right">
                                        <th>Wireless:</th>

                                        <td>{{ item.raw.stock ? 'Yes' : 'No' }}</td>
                                    </tr>

                                    <tr align="right">
                                        <th>Price:</th>

                                        <td>€ {{ item.raw.price }}</td>
                                    </tr>
                                </tbody>
                            </v-table>
                        </v-sheet>
                    </v-col>
                </v-row>
            </template>

            <!-- <template v-slot:footer="{ page, pageCount }">
            <v-footer color="surface-variant" class="justify-space-between text-body-2 mt-4">
                Total mice: {{ prodotti.length }}

                <div>
                    Page {{ page }} of {{ pageCount }}
                </div>
            </v-footer>
        </template> -->
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
            itemsPerPage: 4,
        }
    },
    methods: {
        onClickSeeAll() {
            this.itemsPerPage = this.itemsPerPage === 4 ? this.prodotti.length : 4
        },
    },
    mounted() {
        this.prodotti = prod;
    }
}
</script>

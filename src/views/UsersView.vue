
<template>
    <v-row>
        <v-col>
            <v-card class="mx-auto" max-width="400" style="margin-top: -64px;">
                <v-toolbar flat>
                    <v-toolbar-title class="text-black">
                        Utenti
                    </v-toolbar-title>

                    <v-spacer></v-spacer>
                </v-toolbar>

                <v-divider></v-divider>

                <v-card-text style="max-height: 400px; overflow-y: auto; max-width:400px">
                    <v-scroll-y>
                        <v-list lines="two">
                            <v-list-item v-for="u in utenti" :key="u.id" :title="u.lastName + ' ' + u.firstName"
                                :subtitle="u.email" @click="viewDettagli(u)">
                                <template v-slot:prepend>
                                    <v-avatar :image="u.image"></v-avatar>
                                </template>
                                <!-- 
                                <template v-slot:append>
                                    <v-btn color="grey-lighten-1" icon="mdi-information" variant="text"></v-btn>
                                </template> -->
                                <v-divider inset></v-divider>
                            </v-list-item>
                        </v-list>
                    </v-scroll-y>
                </v-card-text>
            </v-card>
        </v-col>
        <v-col>
            <v-card class="mx-auto" max-width="700" style="margin-top: -64px;">
                <v-toolbar flat>
                    <v-toolbar-title class="text-black">
                        Dettagli
                    </v-toolbar-title>
                    <v-spacer></v-spacer>
                </v-toolbar>
                <v-divider></v-divider>
                <v-card-text style="text-align: left;">
                    <v-row>
                        <v-col>
                            <p><b>Cognome:</b> {{ this.selezionato.lastName }}</p>
                        </v-col>
                        <v-col>
                            <p><b>Nome:</b> {{ this.selezionato.firstName }}</p>
                        </v-col>
                    </v-row>
                    <v-row>
                        <v-col>
                            <p><b>Email:</b> {{ this.selezionato.email }}</p>
                        </v-col>
                        <v-col>
                            <p><b>Telefono:</b> {{ this.selezionato.phone }}</p>
                        </v-col>
                    </v-row>
                    <v-row>
                        <v-col>
                            <p><b>Usarname:</b> {{ this.selezionato.username }}</p>
                        </v-col>
                        <v-col>
                            <v-text-field :append-icon="show2 ? 'mdi-eye' : 'mdi-eye-off'"
                                 :type="show2 ? 'text' : 'password'" name="input-10-2"
                                :value="this.selezionato.password"  class="input-group--focused"
                                @click:append="show2 = !show2" readonly density="compact"></v-text-field>
                        </v-col>
                    </v-row>
                    <v-row>
                        <v-col>
                            <v-expansion-panels>
                                <v-expansion-panel>
                                    <v-expansion-panel-title>
                                        <template v-slot:default="{ expanded }">
                                            <v-row no-gutters>
                                                <v-col cols="4" class="d-flex justify-start">
                                                    Informazioni Personali
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
                                                <p><b>Data di nascita:</b> {{ this.selezionato.birthDate }}</p>
                                            </v-col>
                                            <v-col>
                                                <p><b>Gruppo sanguigno:</b> {{ this.selezionato.bloodGroup }}</p>
                                            </v-col>
                                        </v-row>
                                        <v-row>
                                            <v-col>
                                                <p><b>Altezza:</b> {{ this.selezionato.height }}</p>
                                            </v-col>
                                            <v-col>
                                                <p><b>Peso:</b> {{ this.selezionato.weight }}</p>
                                            </v-col>
                                        </v-row>
                                        <v-row>
                                            <v-col>
                                                <p><b>Colore capelli:</b> {{ this.selezionato.hair.color }}</p>
                                            </v-col>
                                            <v-col>
                                                <p><b>Tipo taglio:</b> {{ this.selezionato.hair.type }}</p>
                                            </v-col>
                                            <v-col>
                                                <p><b>Colore occhi:</b> {{ this.selezionato.eyeColor }}</p>
                                            </v-col>
                                        </v-row>
                                        <v-divider></v-divider>

                                    </v-expansion-panel-text>
                                </v-expansion-panel>


                            </v-expansion-panels>

                        </v-col>
                    </v-row>
                    <v-row>
                        <v-col>
                            <v-expansion-panels>
                                <v-expansion-panel>
                                    <v-expansion-panel-title>
                                        <template v-slot:default="{ expanded }">
                                            <v-row no-gutters>
                                                <v-col cols="4" class="d-flex justify-start">
                                                    Indirizzo
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
                                                <p><b>Indirizzo:</b> {{ this.selezionato.address.address }}</p>
                                            </v-col>
                                            <v-col>
                                                <p><b>Città:</b> {{ this.selezionato.address.city }}</p>
                                            </v-col>
                                        </v-row>
                                        <v-row>
                                            <v-col>
                                                <p><b>Codice postale:</b> {{ this.selezionato.address.postalCode }}</p>
                                            </v-col>
                                            <v-col>
                                                <p><b>Stato:</b> {{ this.selezionato.address.state }}</p>
                                            </v-col>
                                        </v-row>
                                        <v-divider></v-divider>

                                    </v-expansion-panel-text>
                                </v-expansion-panel>


                            </v-expansion-panels>

                        </v-col>
                    </v-row>
                    <v-row>
                        <v-col>
                            <v-expansion-panels>
                                <v-expansion-panel>
                                    <v-expansion-panel-title>
                                        <template v-slot:default="{ expanded }">
                                            <v-row no-gutters>
                                                <v-col cols="4" class="d-flex justify-start">
                                                    Banca
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
                                                <Front :cardNumber="this.selezionato.bank.cardNumber"
                                                    :cardType="maiuscolo(this.selezionato.bank.cardType)"
                                                    :expiration="this.selezionato.bank.cardExpire"
                                                    :name="this.selezionato.firstName + ' ' + this.selezionato.lastName"
                                                    color="grey">
                                                </Front>
                                            </v-col>
                                        </v-row>
                                        <v-row>
                                            <v-col>
                                                <p><b>Valuta:</b> {{ this.selezionato.bank.currency }}</p>
                                            </v-col>
                                            <v-col>
                                                <p><b>IBAN:</b> {{ this.selezionato.bank.iban }}</p>
                                            </v-col>
                                        </v-row>

                                        <v-divider></v-divider>

                                    </v-expansion-panel-text>
                                </v-expansion-panel>


                            </v-expansion-panels>

                        </v-col>
                    </v-row>
                </v-card-text>
            </v-card>
        </v-col>
    </v-row>
</template>
<script>
import users from '../api/utenti'
/* eslint-disable */
import Front from '../components/Front.vue'
export default {
    name: 'UsersView',
    data() {
        return {
            utenti: [],
            selezionato: {
                "id": 1,
                "firstName": "Terry",
                "lastName": "Medhurst",
                "maidenName": "Smitham",
                "age": 50,
                "gender": "male",
                "email": "atuny0@sohu.com",
                "phone": "+63 791 675 8914",
                "username": "atuny0",
                "password": "9uQFF1Lh",
                "birthDate": "2000-12-25",
                "image": "https://robohash.org/Terry.png?set=set4",
                "bloodGroup": "A-",
                "height": 189,
                "weight": 75.4,
                "eyeColor": "Green",
                "hair": {
                    "color": "Black",
                    "type": "Strands"
                },
                "domain": "slashdot.org",
                "ip": "117.29.86.254",
                "address": {
                    "address": "1745 T Street Southeast",
                    "city": "Washington",
                    "coordinates": {
                        "lat": 38.867033,
                        "lng": -76.979235
                    },
                    "postalCode": "20020",
                    "state": "DC"
                },
                "macAddress": "13:69:BA:56:A3:74",
                "university": "Capitol University",
                "bank": {
                    "cardExpire": "06/22",
                    "cardNumber": "50380955204220685",
                    "cardType": "maestro",
                    "currency": "Peso",
                    "iban": "NO17 0695 2754 967"
                },
                "company": {
                    "address": {
                        "address": "629 Debbie Drive",
                        "city": "Nashville",
                        "coordinates": {
                            "lat": 36.208114,
                            "lng": -86.58621199999999
                        },
                        "postalCode": "37076",
                        "state": "TN"
                    },
                    "department": "Marketing",
                    "name": "Blanda-O'Keefe",
                    "title": "Help Desk Operator"
                },
                "ein": "20-9487066",
                "ssn": "661-64-2976",
                "userAgent": "Mozilla/5.0 (Windows NT 6.1) AppleWebKit/534.24 (KHTML, like Gecko) Chrome/12.0.702.0 Safari/534.24",
                "crypto": {
                    "coin": "Bitcoin",
                    "wallet": "0xb9fc2fe63b2a6c003f1c324c3bfa53259162181a",
                    "network": "Ethereum (ERC20)"
                }
            },
            mostra: false,
            show2: false,
        }
    },
    methods: {
        viewDettagli(sel) {
            this.selezionato = sel;
            console.log(this.selezionato);
        },
        mostraNascondi() {
            let stringa = "";
            if (this.mostra == false) {
                for (let i = 0; i < this.selezionato.password.length; i++) {
                    stringa = stringa + "*"
                }
                this.mostra = true;
            } else {
                stringa = this.selezionato.password;
                this.mostra = false;
            }
            return stringa;
        },
        maiuscolo(str) {
            // Verifica che la stringa non sia vuota
            if (str.length === 0) {
                return str;
            }

            // Restituisci la stringa con la prima lettera in maiuscolo
            return str.charAt(0).toUpperCase() + str.slice(1);
        }

    },
    components: {
        Front,
    },
    mounted() {
        this.utenti = users;
    }
}
</script>
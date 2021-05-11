<template>
    <v-col align="center" cols="12" sm="6" offset-sm="3">
        <v-col cols="6">
            <v-select
                v-model="query_param"
                :items="classes"
                menu-props="auto"
                label="Select"
                hide-details
                append-icon="search"
                single-line
                @click:append="alertHello()"
            ></v-select>
        </v-col>
        <v-spacer></v-spacer>

        <v-card>
            <v-container fluid>
                <v-row>
                    <v-col
                        v-for="n in result"
                        :key="n.id"
                        class="d-flex child-flex"
                        cols="4"
                    >
                        <v-card flat tile class="d-flex">
                            <v-img
                                :src="n.thumbnail"
                                aspect-ratio="1"
                                class="grey lighten-2"
                            >
                                <template v-slot:placeholder>
                                    <v-row
                                        class="fill-height ma-0"
                                        align="center"
                                        justify="center"
                                    >
                                        <v-progress-circular
                                            indeterminate
                                            color="grey lighten-5"
                                        ></v-progress-circular>
                                    </v-row>
                                </template>
                            </v-img>
                        </v-card>
                    </v-col>
                </v-row>
            </v-container>
        </v-card>
    </v-col>
</template>

<script>
import axios from "axios";
export default {
    data() {
        return {
            file: "",
            result: null,
            query_param: "",
            classes: ["zebra", "dog", "bird"],
        };
    },
    mounted() {
        this.loadFile();
    },
    methods: {
        handleFileUpload() {
            this.file = this.$refs.file.files[0];
            this.file.fileurl = URL.createObjectURL(this.file);
        },
        alertHello() {
            alert("Hello world");
        },
        loadFile() {
            axios
                .get("http://localhost:8000/image")
                .then((response) => {
                    this.result = response.data;
                    console.log("SUCCESS!!");
                })
                .catch(function () {
                    console.log("FAILURE!!");
                });
        },
    },
};
</script>

<template>
    <v-container>
        <v-col class="justify-center">
            <v-card class="mx-auto my-12 pa-10" max-width="500px">
                <v-img :src="file.fileurl" aspect-ratio="1"> </v-img>
                <v-card-actions class="align-end">
                    <v-btn color="primary" text>
                        <input
                            type="file"
                            id="file"
                            ref="file"
                            v-on:change="handleFileUpload()"
                        />
                    </v-btn>

                    <v-btn color="primary" text @click="submitFile">
                        Upload
                    </v-btn>
                    <v-spacer></v-spacer>
                </v-card-actions>
            </v-card>
        </v-col>
    </v-container>
</template>

<script>
import axios from "axios";
export default {
    data() {
        return {
            file: "",
            result: null,
        };
    },
    methods: {
        handleFileUpload() {
            this.file = this.$refs.file.files[0];
            this.file.fileurl = URL.createObjectURL(this.file);
        },
        submitFile() {
            let formData = new FormData();
            formData.append("image", this.file);
            axios
                .post("http://localhost:8000/image", formData)
                .then((response) => {
                    console.log(response.data);
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

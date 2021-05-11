<template>
    <div id="app">
        <v-app>
            <v-app-bar flat>
                <v-toolbar-title>MicroTag</v-toolbar-title>
                <v-spacer></v-spacer>

                <template v-slot:extension>
                    <v-tabs align-with-title>
                        <v-tab to="/gallery">Gallery</v-tab>
                        <v-tab to="/upload">Add Image</v-tab>
                    </v-tabs>
                </template>
            </v-app-bar>
            <v-app>
                <router-view />
            </v-app>
        </v-app>
    </div>
</template>

<script>
export default {
    name: "App",

    data: () => ({
        //
    }),
};
</script>

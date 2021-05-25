<template>
    <div class="d-flex justify-space-between">
        <div class="d-flex">
            <v-btn text icon to="/apps" class="mr-2">
                <v-icon dark color="white">
                    mdi-apps
                </v-icon>
            </v-btn>
            <v-btn text :to="to">
                <b class="white--text">
                    {{title}}
                </b>
            </v-btn>
            <div class="ml-12" v-if="menu">
                <v-btn text
                    v-for="(item, index) in menu"
                    :key="index"
                    :to="item.link">
                    <b class="white--text">
                        {{ item.nama }}
                    </b>
                </v-btn>
            </div>
        </div>
        <v-btn text>
            <v-icon dark color="white" left>
                mdi-account-circle
            </v-icon>
            <span class="white--text">
                Admin
            </span>
        </v-btn>
    </div>
</template>
<script>
export default {
    props: ['title', 'to', 'menu']
}
</script>
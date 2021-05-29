<template>
    <v-col :sm="sm" :md="md">
        <v-card class="border--primary">
            <v-card-title>
                <p class="subtitle-2 mb-0">{{ title }}</p>
            </v-card-title>
            <v-card-text>
                <div class="text-h3 text-center black--text">{{ value }}</div>
            </v-card-text>
        </v-card>
    </v-col>
</template>
<script>
export default {
    props: ['title', 'value', 'sm', 'md']
}
</script>
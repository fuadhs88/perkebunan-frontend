<template>
    <v-form ref="form">
        <div 
            v-for="(item, index) in fields.filter((item)=>item.form!=false)"
            :key="index">
            <!-- jika tipenya switct -->
            <v-switch 
                v-if="item.type==='switch'"
                :label="item.text"
                v-model="item.status" 
                class="mt-0" />
            <!-- jika tipenya number -->
            <v-text-field
                v-else-if="item.type==='number'"
                type="number"
                :label="item.text"
                :messages="item.info"
                placeholder="tes"/>
            <!-- jika tipenya text -->
            <v-text-field
                v-else
                :label="item.text"
                :messages="item.info"
                placeholder="tes"/>
        </div>
    </v-form>
</template>
<script>
export default {
    props: ['fields']
}
</script>
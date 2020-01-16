<template>
    <div>
        <input type="text" v-model="searchInput"/>
    </div>
</template>

<script>
    import { ref, watch } from '@vue/composition-api'
    const eventApi = {
        getEventCount() {
            return [{
                    text: "someResult"
                }]
        }
    }
    export default {

        setup(){
            const searchInput = ref("")
            const results = ref(0);

            watch(() => {
                results.value = eventApi.getEventCount(searchInput.value);
            });

            return { searchInput, results };
        }
    }
</script>

<style lang="scss" scoped>

</style>
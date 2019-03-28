<template>
    <div>
        <h1>The Stock Trader platform.</h1>
        <p>Here you can trade your stocks. You may save & load your data.</p>
        <p>Click on 'End Day' to begin a new day!</p>
        <p>Your funds: {{ funds  | currency }}</p>
    </div>
</template>

<script>
    export default {
        computed: {
            funds() {
                return this.$store.getters.funds;
            }
        }
    }
</script>

<template>
    <div class="container">
        <app-header></app-header>
        <div class="row">
            <div class="col-xs-12">
                <transition name="fade" mode="out-in">
                    <router-view></router-view>
                </transition>
            </div>
        </div>
    </div>
</template>

<script>
    import appHeader from './components/Header.vue'

    export default {
        components: {
            appHeader
        },
        created() {
            this.$store.dispatch('initStocks');
        }
    }
</script>

<style>
    body {
        padding: 30px;
    }

    .fade-enter-active,
    .fade-leave-active {
        transition: opacity .25s;
    }
    .fade-enter,
    .fade-leave-to {
        opacity: 0;
    }
</style>

<template>
    <div>
        <nav class="navbar navbar-default">
            <div class="container-fluid">
                <div class="navbar-header">
                    <router-link class="navbar-brand" to="/"><strong><i class="fas fa-business-time"></i> Stock Trader</strong></router-link>
                </div>
                <div class="collapse navbar-collapse" id="navbarSupportedContent">
                    <ul class="navbar-nav nav">
                        <router-link to="/stocks" tag="li" activeClass="active"><a>Stocks</a></router-link>
                        <router-link to="/portfolio" tag="li" activeClass="active"><a>Portfolio</a></router-link>
                    </ul>
                    <strong class="navbar-text navbar-right"><i class="fas fa-money-bill-wave"></i> {{ funds | currency }}</strong>
                    <ul class="navbar-nav nav navbar-right">
                        <li><a href="#" @click="endDay"><i class="fas fa-hourglass-end"></i> End day</a></li>
                        <li class="nav-item dropdown" :class="{open: isDropdownOpen}" @click="isDropdownOpen = !isDropdownOpen">
                            <a class="dropdown-toggle" href="#" id="navbarDropdown" role="button" data-toggle="dropdown" aria-haspopup="true" aria-expanded="false">
                                <i class="fas fa-save"></i> Save & load
                            </a>
                            <ul class="dropdown-menu">
                                <li><a class="dropdown-item" href="#" @click="saveData">Save data</a></li>
                                <li><a class="dropdown-item" href="#" @click="loadData">Load data</a></li>
                            </ul>
                        </li>
                    </ul>
                </div>
            </div>
        </nav>
    </div>
</template>

<script>
    import {mapActions} from 'vuex';

    export default {
        data() {
            return {
                isDropdownOpen: false
            }
        },
        computed: {
            funds() {
                return this.$store.getters.funds;
            }
        },
        methods: {
            ...mapActions({
                randomizeStocks: 'randomizeStocks',
                fetchData: 'loadData'
            }),
            endDay() {
                this.randomizeStocks();
            },
            saveData() {
                const data = {
                    funds: this.$store.getters.funds,
                    stockPortfolio: this.$store.getters.stockPortfolio,
                    stocks: this.$store.getters.stocks
                };

                this.$http.put('data.json', data);
            },
            loadData() {
                this.fetchData();
            }
        }
    }
</script>

<style scoped>
    .navbar {
        background: #d4af37;
    }

    .navbar-default .navbar-nav>.active >a,
    .navbar-default .navbar-nav>.active >a:focus,
    .navbar-default .navbar-nav>.active >a:hover {
        background-color: #c3a132;
        color: #000;
    }

    .navbar-default .navbar-text,
    .navbar-default .navbar-brand,
    .navbar-default .navbar-nav >li >a {
        color: #333;
    }

    .navbar-default .navbar-nav >li >a:focus,
    .navbar-default .navbar-nav >li >a:hover {
        color: #000;
    }

    .navbar-default .navbar-nav >.open >a,
    .navbar-default .navbar-nav >.open >a:focus,
    .navbar-default .navbar-nav >.open >a:hover {
        background-color: #c3a132;
        color: #000;
    }
</style>

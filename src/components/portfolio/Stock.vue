<template>
    <div class="col-sm-6 col-md-4">
        <div class="panel panel-success">
            <div class="panel-heading">
                <div class="panel-title">
                    {{ stock.name }} <small>(Price: {{ stock.price }}) | Quantity: {{ stock.qty }}</small>
                </div>
            </div>
            <div class="panel-body">
                <div class="pull-left">
                    <input type="number" class="form-control" placeholder="Quantity" :class="{danger: notEnoughQty}" v-model="qty">
                </div>
                <div class="pull-right">
                    <button class="btn btn-success" @click="sellStock" :disabled="notEnoughFunds || qty <= 0">{{ notEnoughQty ? 'Not enough stocks' : 'Sell' }}</button>
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
    .danger {
        border: 1px solid pink;
    }
</style>

<script>
    import {mapActions} from 'vuex';

    export default {
        props: ['stock'],
        data() {
            return {
                qty: 0
            }
        },
        computed: {
            notEnoughQty() {
                return this.qty > this.stock.qty;
            }
        },
        methods: {
            ...mapActions({
                placeOrder: 'sellStock'
            }),
            sellStock() {
                const order = {
                    stockId: this.stock.id,
                    stockPrice: this.stock.price,
                    qty: this.qty
                };

                this.placeOrder(order);
                this.qty = 0;
            }
        },
        created() {
            console.log(this.stock);
        }
    }
</script>

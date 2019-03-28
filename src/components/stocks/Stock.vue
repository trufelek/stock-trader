<template>
    <div class="col-sm-6 col-md-4">
       <div class="panel panel-warning">
           <div class="panel-heading">
               <div class="panel-title">
                   {{ stock.name }} <small>(Price: {{ stock.price }})</small>
               </div>
           </div>
           <div class="panel-body">
               <div class="pull-left">
                   <input type="number" class="form-control" placeholder="Quantity" :class="{danger: notEnoughFunds}" v-model="qty">
               </div>
               <div class="pull-right">
                   <button class="btn btn-warning" @click="buyStock" :disabled="notEnoughFunds || qty <= 0">{{ notEnoughFunds ? 'Not enough funds' : 'Buy' }}</button>
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
    export default {
        props: ['stock'],
        data() {
            return {
                qty: 0
            }
        },
        computed: {
            funds() {
                return this.$store.getters.funds;
            },
            notEnoughFunds() {
                return this.qty * this.stock.price > this.funds;
            }
        },
        methods: {
            buyStock() {
                const order = {
                    stockId: this.stock.id,
                    stockPrice: this.stock.price,
                    qty: this.qty
                };

                this.$store.dispatch('buyStock', order);

                this.qty = 0;
            }
        }
    }
</script>

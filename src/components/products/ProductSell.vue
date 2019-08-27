<template>
    <div>
        <div class="container">
            
            
    <div class="row">
        <div class="col-6 offset-3 pt-3 card mt-5 shadow">
            <div class="card-body">
                <h3>Product Sell</h3>
                <hr>
                <div class="form-group">
                    <label>Product Name</label>
                    <select class="form-control" v-model="selectedProduct" @change="productSelected">
                        <option selected disabled>Please select a product...</option>
                        <option 
                        :disabled="product.count == 0"
                        :value="product.key"
                        v-for="product in getProducts" :key="product.id">{{product.title}}</option>
                        
                    </select>
                </div>
                <transition name="fade" mode="out-in">
                    <div class="card mb-2 border border-danger" v-if="product !== null">
                    <div class="card-body">
                        <div class="row">
                            <div class="col-12 text-center">
                                <div class="mb-3">
                                    <span class="badge badge-info">Stock : {{product.count}}</span>
                                    <span class="badge badge-primary">Price : {{product.price | currency}}</span>
                                </div>
                                <p class="border border-warning p-2 text-secondary">{{product.description}}</p>
                            </div>
                        </div>
                    </div>
                </div>
                </transition>
                <div class="form-group">
                    <label>Number</label>
                    <input type="text" v-model="product_count" class="form-control" placeholder="Enter product number..">
                </div>
                <hr>
                <button @click="save" class="btn btn-primary">Buy</button>
            </div>
        </div>
    </div>
</div>
    </div>
</template>


<script>
import { mapGetters } from "vuex"
export default {
    data(){
        return{
            selectedProduct: null,
            product : null
        }
    },
    computed:mapGetters(["getProducts"]),
    methods: {
        productSelected(){
           this.product =  this.$store.getters.getProduct(this.selectedProduct)[0];
        },
        save(){
           let product = {
               key : this.selectedProduct,
               count : this.product_count
           }
           this.$store.dispatch("sellProduct", product) 
        },
        beforeRouteLeave (to, from, next) {
        if(this.selectedProduct !== null || this.product_count > 0){
            if(confirm("kaydedilmemis degisiklikler var. Yinede cikmak istiyor musunuz?")){
                next();
            }else{
            next(false);
            }
        }else{
        next();
        }
    }
    
}}

</script>


<style scoped>
     .border-danger {
            border-style: dashed !important;
        }
</style>
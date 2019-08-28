<template>
    <div>
        <div class="container">
            <div class="loading" :style="isLoading">
                <div class="lds-ripple">
                <div></div>
                 <div></div>
            </div>
</div>
    <div class="row">
        <div class="col-6 offset-3 pt-3 card mt-5 shadow">
            <div class="card-body">
                <h3>Product Purchase</h3>
                <hr>
                <div class="form-group">
                    <label>Product Name</label>
                    <input v-model="product.title" type="text" class="form-control" placeholder="Enter product name..">
                </div>
                <div class="form-group">
                    <label>Number</label>
                    <input v-model="product.count" type="number" class="form-control" placeholder="Enter product number..">
                </div>
                <div class="form-group">
                    <label>Price</label>
                    <input v-model="product.price" type="number" class="form-control" placeholder="Enter product price..">
                </div>
                <div class="form-group">
                    <label>Description</label>
                    <textarea v-model="product.description" cols="30" rows="5" placeholder="Enter a description of the product..."
                              class="form-control"></textarea>
                </div>
                <hr>
                <button class="btn btn-primary" :disabled="saveEnabled" @click="saveProduct">Save</button>
                <div style="width:100px; height:100px; margin-top:100px;"></div>
            </div>
        </div>
    </div>
</div>
    </div>
</template>


<script>
export default {
    data(){
        return{
            product: {
                title : "",
                count: null,
                price: null,
                description: "",
            },
            saveButtonClicked: false
        }
    },
    methods:{
        saveProduct(){
            this.saveButtonClicked = true;
            this.$store.dispatch("saveProduct", this.product)
        }
    },
    computed: {
        // button active or passive
        saveEnabled(){
            if(this.product.title.length > 0 && this.product.count.length > 0 && this.product.price.length > 0 && this.product.description.length > 0){
                return false;

            }else{
                return true;
            }
        },
        isLoading(){
            if(this.saveButtonClicked){
                return {
                    display: "block"
                }
            }else{
                return {
                    display : "none"
                }
            }
        }

    },
    //save etmeden cixmamaq ucun bildiris
    beforeRouteLeave (to, from, next) {
        if((this.product.title.length > 0 || this.product.count.length > 0 || this.product.price.length > 0 || this.product.description.length > 0) && !this.saveButtonClicked){
            if(confirm("There are unsaved changes. Do you want to go out anyway?")){
                next();
            }else{
            next(false);
            }
        }else{
        next();
        }
}}
</script>


<style>
    
</style>
<template lang="html">
    <div class="table-responsive">
        <table class="table ps-table">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Image</th>
                    <th>Name</th>
                    <th>SKU</th>
                    <!-- <th>Stock</th> -->
                    <th>Price</th>
                    <th>Categories</th>
                    <th>Transactions</th>                
                </tr>
            </thead>
            <tbody>
                <tr v-for="product in products" :key="product.id">
                    <td>
                        <p> {{product.id}} </p> 
                    </td>           
                    <td>
                        <img width="150" :src="'http://127.0.0.1:8000/storage/products/' + product.file">
                    </td>           
                    <td>
                        <p href="#">
                            <strong>{{ product.product_name }}</strong>
                        </p>
                    </td>
                    <td> <p> {{ product.sku }} </p></td>
                    <!-- <td>
                        <p> {{ product.quantity }} </p>
                    </td> -->
                    <td>
                        <strong>{{ product.price }}</strong>
                    </td>
                    <td>
                        <p class="ps-item-categories">
                                {{product.category_name}}                                        
                        </p>
                    </td>
                    <td>
                        <a href="#">
                            <i class="icon-pencil mr-2"> Edit</i>
                        </a>
                        <a href="#" v-on:click.prevent="deleteProducts(product)">
                            <i class="icon-trash2 mr-2"> Delete</i>
                        </a>
                    </td>
                </tr>
            </tbody>
        </table>
        <div class="ps-section__footer">
            <ul class="pagination">
                <li>
                    <a href="#" @click="pagination.page--; listProducts();">
                        <i class="icon icon-chevron-left"></i>
                    </a>
                </li>
                <li class="active" v-for="n in products.last_page" :key="n" :class="{active:pagination.page==n}">
                    <a href="#" @click="pagination.page=n; listProducts();">{{n}}</a>
                </li>
                <li>
                    <a href="#" @click="pagination.page++; listProducts();">
                        <i class="icon-chevron-right"></i>
                    </a>
                </li>
            </ul>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    name: 'TableProductItems',
    created: function() {
        this.listProducts();
        this.listCategories();
    },
    data() {
        return {
            products:[], 
            errors:[],
            pagination:{
                page:1,
                per_page:5
            },
            form:{
                product_name:"",
                product_slug:"",
                quantity:"",
                price:"",
                discount_rate:"",
                description:"",
                sku:"",
                file:"",
            },
            categories:[], 
        };
    },
    methods: {
    listProducts: function(){
        var url = 'http://127.0.0.1:8000/api/admin/products'
        axios.get(url,{params: this.pagination}).then(response => {
                this.products = response.data.data
        });
    },
    deleteProducts: function(products) {
        var url = 'http://127.0.0.1:8000/api/admin/products/' + products.id;
        axios.delete(url).then(response => {
        });
        this.listProducts()
    },
    updateProducts: function(products){
        var url = ('http://127.0.0.1:8000/api/admin/products/' + products.id);
        axios.put(url,this.form).then(response => {
            console.log(url,this.form)
            });
    },
    closeModal() {
            this.show = false;
            document.querySelector("body").classList.remove("overflow-hidden");
    },
    openModal(products) {
            this.show = true;
            this.products.id=products.id
            this.form.name=products.name
            this.form.email=products.email
            this.form.password=products.password
            document.querySelector("body").classList.add("overflow-hidden");
    },
    listCategories: function(){
            var url = 'http://127.0.0.1:8000/api/admin/categories/'
            axios.get(url,{params: this.pagination}).then(response => {
                    this.categories = response.data.data
            });
        },
    
}
};
</script>

<style lang="scss" scoped></style>

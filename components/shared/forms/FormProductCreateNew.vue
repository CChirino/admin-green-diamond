<template lang='html'>
    <form
        class="ps-form ps-form--new-product"
        v-on:submit.prevent="submitForm" enctype="multipart/form-data" >
        <div class="ps-form__content">
            <div class="row">
                <div class="col-xl-6 col-lg-6 col-md-12 col-sm-12 col-12">
                    <figure class="ps-block--form-box">
                        <figcaption>General</figcaption>
                        <div class="ps-block__content">
                            <div class="form-group">
                                <label>
                                    Product Name<sup>*</sup>
                                </label>
                                <input
                                    class="form-control"
                                    type="text"
                                    placeholder="Enter product name..."
                                    v-model="form.product_name"
                                />
                                <span class="text-danger" v-if="errors.product_name"> {{errors.product_name[0]}} </span>
                            </div>
                            <div class="form-group">
                                <label>
                                    Product slug<sup>*</sup>
                                </label>
                                <input
                                    class="form-control"
                                    type="text"
                                    placeholder="Enter product Slug..."
                                    v-model="form.product_slug"
                                />
                                <span class="text-danger" v-if="errors.product_slug"> {{errors.product_slug[0]}} </span>
                            </div>
                            <div class="form-group">
                                <label>
                                    Regular Price<sup>*</sup>
                                </label>
                                <input
                                    class="form-control"
                                    type="text"
                                    placeholder=""
                                    v-model="form.price"
                                />
                                <span class="text-danger" v-if="errors.price"> {{errors.price[0]}} </span>
                            </div>
                            <!-- <div class="form-group">
                                <label>
                                    Sale Price<sup>*</sup>
                                </label>
                                <input
                                    class="form-control"
                                    type="text"
                                    placeholder=""
                                />
                            </div> -->
                            <!-- <div class="form-group">
                                <label>
                                    Discount<sup>*</sup>
                                </label>
                                <input
                                    class="form-control"
                                    type="text"
                                    placeholder=""
                                    v-model="form.discount_rate"
                                />
                                <span class="text-danger" v-if="errors.discount_rate"> {{errors.discount_rate[0]}} </span>
                            </div> -->
                            <!-- <div class="form-group">
                                <label>
                                    Stock<sup>*</sup>
                                </label>
                                <input
                                    class="form-control"
                                    type="text"
                                    placeholder=""
                                    v-model="form.quantity"
                                />
                                <span class="text-danger" v-if="errors.quantity"> {{errors.quantity[0]}} </span>
                            </div> -->
                            <!-- <div class="form-group">
                                <label>
                                    Sold Items<sup>*</sup>
                                </label>
                                <input
                                    class="form-control"
                                    type="text"
                                    placeholder=""
                                />
                            </div> -->
                            <div class="form-group">
                                <label>
                                    Product Description<sup>*</sup>
                                </label>
                                <textarea
                                    class="form-control"
                                    rows="6"
                                    name="editordata"
                                    v-model="form.description">
                                </textarea>
                            </div>
                        </div>
                    </figure>
                </div>
                <div class="col-xl-6 col-lg-6 col-md-12 col-sm-12 col-12">
                    <figure class="ps-block--form-box">
                        <figcaption>Product Image</figcaption>
                        <div class="ps-block__content">
                                <div class="form-group--nest">
                                    <input
                                        class="form-control mb-1"
                                        placeholder=""
                                        type="file" id="file" ref="file" v-on:change="onChangeFileUpload()"
                                    />
                                    <button class="ps-btn ps-btn--sm">
                                        Choose
                                    </button>
                                </div>                        </div>
                    </figure>
                    <figure class="ps-block--form-box">
                        <figcaption>Inventory</figcaption>
                        <div class="ps-block__content">
                            <div class="form-group">
                                <label>
                                    SKU<sup>*</sup>
                                </label>
                                <input
                                    class="form-control"
                                    type="text"
                                    placeholder=""
                                    v-model="form.sku"
                                />
                            </div>
                            <div class="form-group form-group--select">
                                <label>Select Category</label>
                                <div class="form-group__content">
                                    <select
                                        class="ps-select"
                                        title="Status"                                     
                                        v-model="form.categories_id">
                                        
                                        <option placeholder="Select Category" v-for="categories in categories" :key="categories.id" :value="categories.id">
                                        {{categories.category_name}}                                        
                                        </option>
                                    </select>
                                </div>
                            </div>
                        </div>
                    </figure>
                </div>
            </div>
        </div>
        <div class="ps-form__bottom">
            <a
                class="ps-btn ps-btn--black"
                href="products.html">
                Back
            </a>
            <button class="ps-btn ps-btn--gray">Cancel</button>
            <button class="ps-btn">Submit</button>
        </div>
    </form>
</template>

<script>
import axios from 'axios';
import UploadsFile from "~/components/shared/forms/UploadsFile";

export default {
    name: 'FormProductCreateNew',
        components: {
            UploadsFile,
        },
    created: function() {
        this.listCategories();
    },
    data(){
        return{
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
            errors:{},
            categories:[], 
        }
    },
    methods:{
        submitForm(){
                let formData = new FormData();
                formData.append("product_name", this.form.product_name);
                formData.append("product_slug", this.form.product_slug);
                // formData.append("quantity", this.form.quantity);
                formData.append("price", this.form.price);
                // formData.append("discount_rate", this.form.discount_rate);
                formData.append("description", this.form.description);
                formData.append("sku", this.form.sku);
                formData.append("file", this.form.file);
                formData.append("categories_id", this.form.categories_id);
            axios.post('http://127.0.0.1:8000/api/admin/products', formData)
            .then((res) => {
                     //Perform Success Action
                    console.log(res);
                    // location.reload();
                    window.location.replace("http://localhost:4003/products/");
                 })
                 .catch((error) => {
                     if(error.response.data){
                         this.errors = error.response.data.errors
                     }
                      console.log(error.response.data)
                 }).finally(() => {
                 });
        },
        resetInput() {
            this.form.product_name = "";    
            this.form.product_slug = "";    
            this.form.price = "";    
         },
        listCategories: function(){
            var url = 'http://127.0.0.1:8000/api/admin/categories/'
            axios.get(url,{params: this.pagination}).then(response => {
                    this.categories = response.data.data
            });
        },
        onImageChange:function(e){
            this.form.file = e.target.files[0];        
        },
        onChangeFileUpload(){
        this.form.file = this.$refs.file.files[0];

      }
    }
};
</script>

<style lang="scss" scoped>

</style>

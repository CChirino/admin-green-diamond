<template lang="html">
    <form class="ps-form ps-form--new"  v-on:submit.prevent="submitForm" >
        <div class="ps-form__content">
            <div class="form-group">
                <label> Name<sup>*</sup> </label>
                <input v-model="form.category_name" class="form-control" type="text" placeholder="Enter category name" />
                <span class="text-danger" v-if="errors.category_name"> {{errors.category_name[0]}} </span>
            </div>
            <div class="form-group">
                <label> Slug<sup>*</sup> </label>
                <input v-model="form.category_slug" class="form-control" type="text" placeholder="Enter category slug" />
                <span class="text-danger" v-if="errors.category_slug"> {{errors.category_slug[0]}} </span>
            </div>
            <!-- <div class="form-group form-group--select">
                <label>Parent</label>
                <div class="form-group__content">
                    <select class="ps-select" title="Parent">
                        <option value="1">Parent 1</option>
                        <option value="2">Parent 2</option>
                        <option value="3">Parent 3</option>
                        <option value="4">Parent 4</option>
                    </select>
                </div>
            </div> -->
            <div class="form-group">
                <label>Description</label>
                    <input v-model="form.category_description" class="form-control" type="text" placeholder="Enter category description" />
                    <span class="text-danger" v-if="errors.category_description"> {{errors.category_description[0]}} </span>
            </div>
        </div>
        <div class="ps-form__bottom">
            <button class="ps-btn ps-btn--gray" @click="resetInput">Reset</button>
            <button class="ps-btn ps-btn--sumbit success">
                Add new
            </button>
        </div>
    </form>
</template>

<script>
import axios from 'axios';
export default {
    name: "FormCreateCategory",
    data(){
        return{
            form:{
                category_name:"",
                category_slug:"",
                category_description:"",
            },
            errors:{}
        }
    },
    methods:{
        submitForm(){
            axios.post('http://127.0.0.1:8000/api/admin/categories', this.form)
                 .then((res) => {
                     //Perform Success Action
                    location.reload();
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
            this.form.category_name = "";    
            this.form.category_slug = "";    
            this.form.category_description = "";    
         },
    }
};
</script>

<style lang="scss" scoped></style>

<template lang="html">
    <form class="ps-form ps-form--new"  v-on:submit.prevent="submitForm">
        <div class="ps-form__content">
            <div class="form-group">
                <label> Name<sup>*</sup> </label>
                <input v-model="form.name" class="form-control" type="text" placeholder="Enter name" />
                <span class="text-danger" v-if="errors.name"> {{errors.name[0]}} </span>
            </div>
            <div class="form-group">
                <label> Slug<sup>*</sup> </label>
                <input v-model="form.slug" class="form-control" type="text" placeholder="Enter Slug" />
                <span class="text-danger" v-if="errors.slug"> {{errors.slug[0]}} </span>
            </div>
            <div class="form-group">
                <label> Description<sup>*</sup> </label>
                <input v-model="form.description" class="form-control" type="text" placeholder="Enter Description" />
                <span class="text-danger" v-if="errors.description"> {{errors.description[0]}} </span>
            </div>
        </div>
        <div class="ps-form__bottom">
            <button class="ps-btn ps-btn--sumbit success">
                Add new
            </button>
        </div>
    </form>
</template>

<script>
import axios from 'axios';
export default {
    name: "FormPermissionCreate",
    data(){
        return{
            form:{
                name:"",
                slug:"",
                description:"",
            },
            errors:{}
        }
    },
    methods:{
        submitForm(){
            axios.post('http://127.0.0.1:8000/api/admin/permission', this.form)
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
        }
    }
}
</script>

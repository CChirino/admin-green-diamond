<template lang="html">
    <form class="ps-form ps-form--new"  v-on:submit.prevent="submitForm">
        <div class="ps-form__content">
            <div class="form-group">
                <label> Name<sup>*</sup> </label>
                <input v-model="form.name" class="form-control" type="text" placeholder="Enter name" />
                <span class="text-danger" v-if="errors.name"> {{errors.name[0]}} </span>
            </div>
            <div class="form-group">
                <label> Email<sup>*</sup> </label>
                <input v-model="form.email" class="form-control" type="email" placeholder="Enter Email" />
                <span class="text-danger" v-if="errors.email"> {{errors.email[0]}} </span>
            </div>
            <div class="form-group">
                <label> Password<sup>*</sup> </label>
                <input v-model="form.password" class="form-control" type="password" placeholder="Enter Password" />
                <span class="text-danger" v-if="errors.password"> {{errors.password[0]}} </span>
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
    name: "FormSupervisorCreate",
    data(){
        return{
            form:{
                name:"",
                email:"",
                password:"",
            },
            errors:{}
        }
    },
    methods:{
        submitForm(){
            axios.post('http://127.0.0.1:8000/api/admin/supervisor', this.form)
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
};
</script>

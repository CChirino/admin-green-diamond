<template lang="html">
    <form class="ps-form ps-form--new"  v-on:submit.prevent="submitForm">
        <div class="ps-form__content">
            <div class="form-group">
                <label> Name<sup>*</sup> </label>
                <input v-model="form.name" class="form-control" type="text" placeholder="Enter name" />
                <span class="text-danger" v-if="errors.name"> {{errors.name[0]}} </span>
            </div>
            <div class="form-group">
                <label> Description<sup>*</sup> </label>
                <input v-model="form.description" class="form-control" type="text" placeholder="Enter Description" />
                <span class="text-danger" v-if="errors.description"> {{errors.description[0]}} </span>
            </div>
            <div class="form-group">
                <label> Full Access<sup>*</sup> </label>
                <div class="form-check">
                    <input v-model="form.full_access" class="form-check-input" type="radio" name="full_access" id="full_access" value="yes" >
                    <label class="form-check-label" for="full_access">
                        Yes
                    </label>
                </div>
                <div class="form-check">
                    <input v-model="form.full_access" class="form-check-input" type="radio" name="full_access" id="full_access" value="no">
                    <label class="form-check-label" for="full_access">
                        No
                    </label>
                </div>
                <span class="text-danger" v-if="errors.full_access"> {{errors.full_access[0]}} </span>
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
    name: "FormRoleCreate",
    data(){
        return{
            form:{
                name:"",
                description:"",
                full_access:"",
                },
            errors:{}
        }
    },
    methods:{
        submitForm(){
            axios.post('http://207.244.228.155/api/admin/roles', this.form)
                 .then((res) => {
                     //Perform Success Action
                        location.reload();

                 })
                 .catch((error) => {
                      console.log(error.response.data)
                 }).finally(() => {
                 });
        }
    }
};
</script>

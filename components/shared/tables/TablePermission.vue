<template lang="html">
    <div class="table-responsive">
        <table class="table ps-table">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Name</th>
                    <th>Slug</th>
                    <th>Description</th>
                    <th>Created at</th>
                    <th>Transactions</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="permissions in permissions" :key="permissions.id">
                    <td>
                        <p> {{permissions.id}} </p> 
                    </td>
                    <td>
                        <p> {{permissions.name}} </p> 
                    </td>
                    <td>
                        <p> {{permissions.slug}} </p> 
                    </td>
                    <td>                       
                         <p> {{permissions.description}} </p> 
                    </td>
                    <td>
                        <p> {{permissions.created_at}} </p> 
                    </td>
                    <td>
                            <i class="icon-pencil mr-2" v-on:click.prevent="openModal(permissions);" style="cursor: pointer;"> Edit </i>
                        <a href="#"  ><!--$refs.modal.openModal()-->
                        </a>
                        <a href="#" v-on:click.prevent="deletePermission(permissions)">
                            <i class="icon-trash2 mr-2"> Delete</i>
                        </a>
                    </td>
                </tr> 
            </tbody>
        </table>
        <div class="ps-section__footer">
            <ul class="pagination">
                <li>
                    <a href="#" @click="pagination.page--; listPermission();">
                        <i class="icon icon-chevron-left"></i>
                    </a>
                </li>
                <li class="active" v-for="n in permissions.last_page" :key="n" :class="{active:pagination.page==n}">
                    <a href="#" @click="pagination.page=n; listPermission();">{{n}}</a>
                </li>
                <li>
                    <a href="#" @click="pagination.page++; listPermission();">
                        <i class="icon-chevron-right"></i>
                    </a>
                </li>
            </ul>
        </div>
        <transition name="fade">
        <div class="" v-if="show">
        <div class="modal-container">
            <div class="modal-content">
            <span @click="closeModal()" class="close">&times;</span>
                <form class="ps-form ps-form--new"  v-on:click.prevent="updatePermission(permissions)">
                <div class="ps-form__content">
                    <div class="form-group">
                        <input v-model="permissions.id" class="form-control" type="hidden"/>
                    </div>
                    <div class="form-group">
                        <label> Name<sup>*</sup> </label>
                        <input v-model="form.name" class="form-control" type="text" placeholder="Enter name" />
                    </div>
                    <div class="form-group">
                        <label> Slug<sup>*</sup> </label>
                        <input v-model="form.slug" class="form-control" type="text" placeholder="Enter Slug" />
                    </div>
                    <div class="form-group">
                        <label> Description<sup>*</sup> </label>
                        <input v-model="form.description" class="form-control" type="text" placeholder="Enter Description" />
                    </div>
                </div>
                <div class="ps-form__bottom">
                    <button class="ps-btn ps-btn--sumbit success">
                        Update
                    </button>
                </div>
                </form>
            </div>

        </div>
        </div>
    </transition>
    </div>
</template>
<script>
import axios from 'axios';
import Modal from "~/components/shared/modals/Modal";
export default {
    name: "TablePermission",
    created: function() {
        this.listPermission();
    },
    components: {
        Modal,
    },
    data() {
        return{
            permissions:[], 
            errors:[],
            show: false,
             form:{
                name:"",
                slug:"",
                description:"",
            },
            pagination:{
                page:1,
                per_page:5
            }
            
        }
    },
    methods: {
    listPermission: function(){
        var url = 'http://127.0.0.1:8000/api/admin/permission'
        axios.get(url,{params: this.pagination}).then(response => {
                this.permissions = response.data.data
        });
    },
    deletePermission: function(permissions) {
        var url = 'http://127.0.0.1:8000/api/admin/permission' + permissions.id;
        axios.delete(url).then(response => {
        });
        this.listPermission()
    },
    updatePermission: function(permissions){
        var url = ('http://127.0.0.1:8000/api/admin/permission/' + permissions.id);
        axios.put(url,this.form).then(response => {
            console.log(url,this.form)
            });
    },
    closeModal() {
            this.show = false;
            document.querySelector("body").classList.remove("overflow-hidden");
    },
    openModal(permissions) {
            this.show = true;
            this.permissions.id =permissions.id
            this.form.name =permissions.name
            this.form.slug =permissions.slug
            this.form.description =permissions.description
            document.querySelector("body").classList.add("overflow-hidden");
    },
    
    
}
};
</script>

<style scoped>
.modal-container {
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */
  background-color: rgb(0,0,0); /* Fallback color */
  background-color: rgba(0,0,0,0.4); /* Black w/ opacity */
}

.modal-content {
  background-color: #fefefe;
  margin: 15% auto; /* 15% from the top and centered */
  padding: 20px;
  border: 1px solid #888;
  width: 80%; /* Could be more or less, depending on screen size */
}
.close {
  color: #aaa;
  float: right;
  font-size: 28px;
  font-weight: bold;
}

.close:hover,
.close:focus {
  color: black;
  text-decoration: none;
  cursor: pointer;
}
</style>
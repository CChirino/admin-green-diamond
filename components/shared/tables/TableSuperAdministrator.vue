<template lang="html">
    <div class="table-responsive">
        <table class="table ps-table">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Name</th>
                    <th>Email</th>
                    <th>Created at</th>
                    <th>Transactions</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="superadministrators in superadministrators" :key="superadministrators.id">
                    <td>
                        <p> {{superadministrators.id}} </p> 
                    </td>
                    <td>
                        <p> {{superadministrators.name}} </p> 
                    </td>
                    <td>                       
                         <p> {{superadministrators.email}} </p> 
                    </td>
                    <td>
                        <p> {{superadministrators.created_at}} </p> 
                    </td>
                    <td>
                            <i class="icon-pencil mr-2" v-on:click.prevent="openModal(superadministrators);" style="cursor: pointer;"> Edit</i>
                        <a href="#"  >
                        </a>
                        <a href="#" v-on:click.prevent="deleteSuperAdministrator(superadministrators)">
                            <i class="icon-trash2 mr-2"> Delete</i>
                        </a>
                    </td>
                </tr> 
            </tbody>
        </table>
        <div class="ps-section__footer">
            <ul class="pagination">
                <li>
                    <a href="#" @click="pagination.page--; listSuperAdministrator();">
                        <i class="icon icon-chevron-left"></i>
                    </a>
                </li>
                <li class="active" v-for="n in superadministrators.last_page" :key="n" :class="{active:pagination.page==n}">
                    <a href="#" @click="pagination.page=n; listSuperAdministrator();">{{n}}</a>
                </li>
                <li>
                    <a href="#" @click="pagination.page++; listSuperAdministrator();">
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
                <form class="ps-form ps-form--new"  v-on:click.prevent="updateSuperAdministrator(superadministrators)">
                <div class="ps-form__content">
                    <div class="form-group">
                        <input v-model="superadministrators.id" class="form-control" type="hidden" placeholder="Enter name" />
                    </div>
                    <div class="form-group">
                        <label> Name<sup>*</sup> </label>
                        <input v-model="form.name" class="form-control" type="text" placeholder="Enter name" />
                    </div>
                    <div class="form-group">
                        <label> Email<sup>*</sup> </label>
                        <input v-model="form.email" class="form-control" type="email" placeholder="Enter Email" />
                    </div>
                    <div class="form-group">
                        <label> Password<sup>*</sup> </label>
                        <input v-model="form.password" class="form-control" type="password" placeholder="Enter Password" />
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
    name: "TableSuperAdministrator",
    created: function() {
        this.listSuperAdministrator();
    },
    components: {
        Modal,
    },
    data() {
        return{
            superadministrators:[], 
            errors:[],
            show: false,
             form:{
                name:"",
                email:"",
                password:"",
            },
            pagination:{
                page:1,
                per_page:5
            }
            
        }
    },
    methods: {
    listSuperAdministrator: function(){
        var url = 'http://127.0.0.1:8000/api/admin/super-administrator/'
        axios.get(url,{params: this.pagination}).then(response => {
                this.superadministrators = response.data.data
        });
    },
    deleteSuperAdministrator: function(superadministrators) {
        var url = 'http://127.0.0.1:8000/api/admin/super-administrator/' + superadministrators.id;
        axios.delete(url).then(response => {
        });
        this.listUser()
    },
    updateSuperAdministrator: function(superadministrators){
        var url = 'http://127.0.0.1:8000/api/admin/super-administrator/' + superadministrators.id;
        axios.put(url,this.form).then(response => {
            console.log(url,this.form)
            });
    },
    closeModal() {
            this.show = false;
            document.querySelector("body").classList.remove("overflow-hidden");
    },
    openModal(superadministrators) {
            this.show = true;
            this.superadministrators.id =superadministrators.id
            this.form.name =superadministrators.name
            this.form.email =superadministrators.email
            this.form.password =superadministrators.password
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
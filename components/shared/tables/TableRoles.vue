<template lang="html">
    <div class="table-responsive">
        <table class="table ps-table">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Name</th>
                    <th>Description</th>
                    <th>Created at</th>
                    <th>Transactions</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="role in roles" :key="role.id">
                    <td>
                        <p> {{role.id}} </p> 
                    </td>
                    <td>
                        <p> {{role.name}} </p> 
                    </td>
                    <td>                       
                         <p> {{role.description}} </p> 
                    </td>
                    <td>
                        <p> {{role.created_at}} </p> 
                    </td>
                    <td>
                            <i class="icon-pencil mr-2" v-on:click.prevent="openModal(roles);" style="cursor: pointer;"> Edit</i>
                        <a href="#"  ><!--$refs.modal.openModal()-->
                        </a>
                        <a href="#" v-on:click.prevent="deleteRole(roles)">
                            <i class="icon-trash2 mr-2"> Delete</i>
                        </a>
                    </td>
                </tr> 
            </tbody>
        </table>
        <div class="ps-section__footer">
            <ul class="pagination">
                <li>
                    <a href="#" @click="pagination.page--; listRole();">
                        <i class="icon icon-chevron-left"></i>
                    </a>
                </li>
                <li class="active" v-for="n in roles.last_page" :key="n" :class="{active:pagination.page==n}">
                    <a href="#" @click="pagination.page=n; listRole();">{{n}}</a>
                </li>
                <li>
                    <a href="#" @click="pagination.page++; listRole();">
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
                <form class="ps-form ps-form--new"  v-on:click.prevent="updateUser(users)">
                <div class="ps-form__content">
                    <div class="form-group">
                        <input v-model="users.id" class="form-control" type="hidden" placeholder="Enter name" />
                    </div>
                    <div class="form-group">
                        <label> Name<sup>*</sup> </label>
                        <input v-model="users.name" class="form-control" type="text" placeholder="Enter name" />
                    </div>
                    <div class="form-group">
                        <label> Email<sup>*</sup> </label>
                        <input v-model="users.email" class="form-control" type="email" placeholder="Enter Email" />
                    </div>
                    <div class="form-group">
                        <label> Password<sup>*</sup> </label>
                        <input v-model="users.password" class="form-control" type="password" placeholder="Enter Password" />
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
    name: "TableRoles",
    created: function() {
        this.listRole();
    },
    components: {
        Modal,
    },
    data() {
        return{
            roles:[], 
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
    listRole: function(){
        var url = 'http://127.0.0.1:8000/api/admin/roles'
        axios.get(url,{params: this.pagination}).then(response => {
                this.roles = response.data.data
        });
    },
    deleteRole: function(roles) {
        var url = 'http://127.0.0.1:8000/api/admin/roles' + roles.id;
        axios.delete(url).then(response => {
        });
        this.listRole()
    },
    updateUser: function(users){
        var url = 'http://127.0.0.1:8000/api/admin/users/' + users.id;
        axios.put(url,this.users).then(response => {
            console.log(url,this.users)
            });
    },
    closeModal() {
            this.show = false;
            document.querySelector("body").classList.remove("overflow-hidden");
    },
    openModal(users) {
            this.show = true;
            this.users.id =users.id
            this.users.name =users.name
            this.users.email =users.email
            this.users.password =users.password
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
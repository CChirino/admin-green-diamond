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
                <tr v-for="supervisors in supervisors" :key="supervisors.id">
                    <td>
                        <p> {{supervisors.id}} </p> 
                    </td>
                    <td>
                        <p> {{supervisors.name}} </p> 
                    </td>
                    <td>                       
                         <p> {{supervisors.email}} </p> 
                    </td>
                    <td>
                        <p> {{supervisors.created_at}} </p> 
                    </td>
                    <td>
                            <i class="icon-pencil mr-2" v-on:click.prevent="openModal(supervisors);" style="cursor: pointer;"> Edit</i>
                        <a href="#"  >
                        </a>
                        <a href="#" v-on:click.prevent="deleteAdministrator(supervisors)">
                            <i class="icon-trash2 mr-2"> Delete</i>
                        </a>
                    </td>
                </tr> 
            </tbody>
        </table>
        <div class="ps-section__footer">
            <ul class="pagination">
                <li>
                    <a href="#" @click="pagination.page--; listSupervisor();">
                        <i class="icon icon-chevron-left"></i>
                    </a>
                </li>
                <li class="active" v-for="n in supervisors.last_page" :key="n" :class="{active:pagination.page==n}">
                    <a href="#" @click="pagination.page=n; listSupervisor();">{{n}}</a>
                </li>
                <li>
                    <a href="#" @click="pagination.page++; listSupervisor();">
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
                <form class="ps-form ps-form--new"  v-on:click.prevent="updateSupervisor(supervisors)">
                <div class="ps-form__content">
                    <div class="form-group">
                        <input v-model="supervisors.id" class="form-control" type="hidden" />
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
    name: "TableSupervisor",
    created: function() {
        this.listSupervisor();
    },
    components: {
        Modal,
    },
    data() {
        return{
            supervisors:[], 
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
    listSupervisor: function(){
        var url = 'http://127.0.0.1:8000/api/admin/supervisor/'
        axios.get(url,{params: this.pagination}).then(response => {
                this.supervisors = response.data.data
        });
    },
    deleteSupervisor: function(supervisors) {
        var url = 'http://127.0.0.1:8000/api/admin/supervisor/' + supervisors.id;
        axios.delete(url).then(response => {
        });
        this.listSupervisor()
    },
    updateSupervisor: function(supervisors){
        var url = ('http://127.0.0.1:8000/api/admin/supervisor/' + supervisors.id);
        axios.put(url,this.form).then(response => {
            console.log(url,this.form)
            });
    },
    closeModal() {
            this.show = false;
            document.querySelector("body").classList.remove("overflow-hidden");
    },
    openModal(supervisors) {
            this.show = true;
            this.supervisors.id =supervisors.id
            this.form.name =supervisors.name
            this.form.email =supervisors.email
            this.form.password =supervisors.password
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
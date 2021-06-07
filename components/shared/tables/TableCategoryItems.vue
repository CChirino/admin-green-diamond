<template lang="html">
    <div class="table-responsive">
        <table class="table ps-table">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Category name</th>
                    <th>Slug</th>
                    <th>Description</th>
                    <th>Transactions</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="categories in categories" :key="categories.id">
                    <td>
                        <p> {{categories.id}} </p> 
                    </td>
                    <td>
                        <p> {{categories.category_name}} </p> 
                    </td>
                    <td>                       
                         <p> {{categories.category_slug}} </p> 
                    </td>
                    <td>
                        <p> {{categories.category_description}} </p> 
                    </td>
                    <td>
                            <i class="icon-pencil mr-2" v-on:click.prevent="openModal(categories);" style="cursor: pointer;"> Edit</i>
                        <a href="#"  >
                        </a>
                        <a href="#" v-on:click.prevent="deleteCategories(categories)">
                            <i class="icon-trash2 mr-2"> Delete</i>
                        </a>
                    </td>
                </tr> 
            </tbody>
        </table>
          <div class="ps-section__footer">
            <ul class="pagination">
                <li>
                    <a href="#" @click="pagination.page--; listCategories();">
                        <i class="icon icon-chevron-left"></i>
                    </a>
                </li>
                <li class="active" v-for="n in categories.last_page" :key="n" :class="{active:pagination.page==n}">
                    <a href="#" @click="pagination.page=n; listCategories();">{{n}}</a>
                </li>
                <li>
                    <a href="#" @click="pagination.page++; listCategories();">
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
                <form class="ps-form ps-form--new"  v-on:click.prevent="updateCategories(categories)">
                <div class="ps-form__content">
                    <div class="form-group">
                        <input v-model="categories.id" class="form-control" type="hidden" />
                    </div>
                    <div class="form-group">
                        <label> Name<sup>*</sup> </label>
                        <input v-model="categories.category_name" class="form-control" type="text" placeholder="Enter category name" />
                    </div>
                    <div class="form-group">
                        <label> Email<sup>*</sup> </label>
                        <input v-model="categories.category_slug" class="form-control" type="email" placeholder="Enter category Email" />
                    </div>
                    <div class="form-group">
                        <label> Password<sup>*</sup> </label>
                        <input v-model="categories.category_description" class="form-control" type="password" placeholder="Enter category description" />
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
export default {
    name: "TableCategoryItems",
    created: function() {
        this.listCategories();
    },
    data() {
        return{
            categories:[], 
            errors:[],
            show: false,
             form:{
                category_name:"",
                category_slug:"",
                category_description:"",
            },
            pagination:{
                page:1,
                per_page:5
            }
            
        }
    },
    methods: {
        listCategories: function(){
            var url = 'http://127.0.0.1:8000/api/admin/categories/'
            axios.get(url,{params: this.pagination}).then(response => {
                    this.categories = response.data.data
            });
        },
        deleteCategories: function(categories) {
            var url = 'http://127.0.0.1:8000/api/admin/categories/' + categories.id;
            axios.delete(url).then(response => {
            });
            this.listCategories()
        },
        updateCategories: function(categories){
            var url = 'http://127.0.0.1:8000/api/admin/categories/' + categories.id;
            axios.put(url,this.categories).then(response => {
                console.log(url,this.categories)
                });
        },
        closeModal() {
                this.show = false;
                document.querySelector("body").classList.remove("overflow-hidden");
        },
        openModal(administrators) {
                this.show = true;
                this.categories.id =categories.id
                this.categories.category_name =categories.category_name
                this.categories.category_slug =categories.category_slug
                this.categories.category_description =categories.category_description
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

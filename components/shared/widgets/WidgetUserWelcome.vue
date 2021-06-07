<template lang='html'>
    <div class="ps-block--user-wellcome">
        <div class="ps-block__left">
            <img src="~/static/img/user/admin.jpg" alt="" />
        </div>
        <div class="ps-block__right">
            <p>
                Hello,<a href="#">Green Diamond </a>
            </p>
            <p  v-for="user in user" :key="user.id"> 
                {{user.name}}
            </p>
        </div>
        <div class="ps-block__action">
            <a href="#">
                <i class="icon-exit"></i>
            </a>
        </div>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    name: 'WidgetUserWelcome',
        created: function() {
        this.userData();
    },
        data() {
        return{
            user:[], 
        }
    },
    methods: {
    userData: function(){
        var url = 'http://127.0.0.1:8000/api/user/'
        axios.get(url).then(response => {
                this.user = response.data.data
        });
        },
    }
};
</script>

<style lang='scss' scoped>

</style>

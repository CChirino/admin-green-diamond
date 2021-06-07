<template>
  <transition name="fade">
    <div class="" v-if="show">
      <div class="modal-container">
        <div class="modal-content">
          <span @click="closeModal()" class="close">&times;</span>
              <form class="ps-form ps-form--new">
              <div class="ps-form__content">
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
</template>

<script>
export default {
    name: "Modal",
    data() {
        return {
            show: false,
            fillUser:{'id':'','keep': ''},
        };
    },
    methods: {
        closeModal() {
            this.show = false;
            document.querySelector("body").classList.remove("overflow-hidden");
        },
        openModal() {
            this.show = true;
            document.querySelector("body").classList.add("overflow-hidden");
        },
    },
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
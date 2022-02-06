<template>
    <div>
        <div class="userDetailsWrapper">
            <div class="left">
                <div class="image">
                    <!-- <img v-bind:src="'../assets/'+userData.img" alt="" height="40"> -->
                    <div>Image</div>
                </div>
                <div>
                    <span class="display_email">{{userData.email}}</span>
                    <span class="display_accessLevel">  ({{userData.access_level}})</span>
                    <div id="display_caption">{{userData.email}}</div>
                </div>
            </div>
            <div class="dot_wrap">
                <button class='dot' @click="showForm=true, setUser(userData)">&#8942;</button>
                <button @click="removeButton(currentUser)" class="removeButton">Remove</button>
            </div>
            <add-user v-if="showForm" :userData="currentUser" v-on:update="updateUser($event)"/>
        </div>
    </div>
</template>

<script>

import Swal from 'sweetalert2';
import AddUser from './AddUser.vue';

export default {
  name: 'User',
  data() {
    return {
      currentUser: {},
      showForm: false,
    };
  },
  props: [
    'userData',
  ],
  components: {
    AddUser,
  },
  methods: {
    setUser(user) {
      this.currentUser = user || {};
    },
    updateUser(user) {
      this.$emit('updateInfo', user);
      this.showForm = false;
    },
    removeButton(user) {
      Swal.fire({
        title: this.userData.email,
        text: 'The above user, Will not be able to access this site',
        icon: 'warning',
        showCancelButton: true,
        confirmButtonColor: '#68a679',
        cancelButtonColor: 'rgba(0,0,0,0.3)',
        confirmButtonText: 'Yes, Remove User!',
      }).then((result) => {
        if (result.isConfirmed) {
          this.remove(user);
          Swal.fire(
            '',
            'User has been removed succesfully',
          );
        }
      }).catch((result) => {
        // return;
      });
    },
    remove(user) {
      console.log(user);
      this.$emit('removeUser', user);
    },
  },
};
</script>

<style scoped>

.display_email {
    font-family: 'Avenir';
    font-size: 15px;
}
.display_accessLevel {
    font-family: 'Avenir';
    font-size: 85%;
    font-style: italic;
    color: #8E8A8A;
}
#display_caption {
    font-size: 75%;
    color: #A9A4A4;
}
.userDetailsWrapper {
    display: flex;
    justify-content: space-between;
    padding: 10px;
}
.dot {
    align-items: right;
    border: none;
    cursor: pointer;
    background: none;
    margin-right: 20px;
}

.dot:hover {
    background: rgba(0,0,0,0.1);
}

.left {
    justify-self: start;
    text-align: start;
    display: flex;
}
.image {
    padding-right: 10px;
}
.removeButton {
    font-weight: bold;
    border: none;
    padding: 12px 25px;
    cursor: pointer;
    border-top-right-radius: 3px ;
    color: rgba(0,0,0,0.5)
}
</style>

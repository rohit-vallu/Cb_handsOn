<template>
    <div class="homePageMain">
        <div class="Head">
            <div>
                <h1>Team Members List ({{count}})</h1>
            </div>
            <div class="invite_wrapper">
                <button id="inviteMember" @click="showForm = true">+ Invite Members</button>
            </div>
        </div>
        <!-- eslint-disable max-len -->
        <add-user v-if="showForm" v-on:userAddition="addUser($event)" v-on:updateInfo="updateUser($event)"/>
        <!-- eslint-disable max-len -->
        <ul class="list">
            <li v-bind:key="User.email" v-for="User in Users">
                <User :userData="User" v-on:removeUser="remove($event)"/>
                <hr>
            </li>
        </ul>
    </div>
</template>

<script>

import User from './User.vue';
import AddUser from './AddUser.vue';

export default {
  name: 'HomePage',
  data() {
    return {
      showForm: false,
      Users: [
        {
          id: 1, access_level: 'Admin', email: 'admin@chargebee.com',
        },
        {
          id: 2, access_level: 'Analyst', email: 'rohit.ganesh@chargebee.com',
        },
      ],
      size: 0,
    };
  },
  computed: {
    count() {
      return this.Users.length;
    },
  },
  methods: {
    addUser(user) {
      /* eslint-disable no-param-reassign */
      user.id = this.size + 1;
      /* eslint-disable no-param-reassign */
      this.Users.push(user);
      this.showForm = false;
    },
    updateUser(user) {
      const index = this.Users.findIndex((el) => el.id === user.id);
      this.Users[index] = user;
    },
    remove(user) {
      const index = this.Users.findIndex((el) => el.id === user.id);
      this.Users.splice(index, 1);
    },
    closePage() {
      this.showForm = false;
    },
  },
  components: {
    User,
    AddUser,
  },
};

</script>

<style scoped>

#inviteMember {
    background-color: #7a28c7;
    border-top-right-radius: 3px ;
    cursor: pointer;
    color: white;
    border: none;
    padding: 12px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    font-weight: bold;
}
ul {
    padding: 0;
}
li{
    list-style: none;
}

.homePageMain {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  max-width: 700px;
  margin: 0 auto;
  text-align: center;
  margin-top: 8%;
  background: rgba(0,0,0,0.1);
  padding: 50px;
}

.list{
    background: white;
}

hr {
    background: rgba(253,100,98,0.1);
    border-width: 0.5px;
}

/* .invite_wrapper {
    justify-content: space-evenly;
} */

.Head {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
</style>

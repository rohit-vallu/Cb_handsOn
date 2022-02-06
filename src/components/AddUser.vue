<template>
    <div class="form_wrapper">
            <form>
                <div class="topContainer">
                    <div class="topleft" v-if="!setUpdateButton">
                        <h1> Invite a team member to use chargebee </h1>
                        <!-- eslint-disable max-len -->
                        <p class="inviteCaption">You can either let your team members access everything in this site, or assigning specific roles to them</p>
                        <!-- eslint-disable max-len -->
                    </div>
                    <h1 v-else class="headButtonUpdate">Change role for {{user.email}}</h1>
                    <div class="topright">
                        <button id="inviteMember" v-on:click.prevent="addUser" v-if="!setUpdateButton">Invite Member</button>
                        <button id="updateMember" v-on:click.prevent="updateUser" v-if="setUpdateButton"> Update </button>
                        <br>
                        <button id="cancel">Cancel</button>
                        <br>
                        <br>
                    </div>
                </div>
                <div v-if="!setUpdateButton" class="email">
                    <label for="email">Email</label><br>
                    <input type="text" id="email" v-model="user.email" size="70">
                    <br><br>
                </div>
                <div class="access">
                    <label for="accessLevel">Select User Access Level</label><br><br>
                    <input type="radio" id="admin" name="role" value="Admin" v-model="user.access_level">
                    <label for="admin">Admin</label><br>
                    <p class="caption">Access Everything at chargebee</p>
                    <hr>
                    <input type="radio" id="techSupport" name="role" value="Tech Support" v-model="user.access_level">
                    <label for="techSupport">Tech Support</label><br>
                    <p class="caption">User can view "Subscriptions" and "Product Catalog" tabs. Can also view, add comments to,
                      send, download individual Invoices / Credit Notes.
                    </p>
                    <hr>
                    <input type="radio" id="analyst" name="role" value="Analyst" v-model="user.access_level">
                    <label for="analyst">Analyst</label><br>
                    <p class="caption">In addition to Tech Support Level access, users will also have access to the SaaS metrics report</p>
                </div>
            </form>
        <!-- </div> -->
    </div>
</template>

<script>

export default {
  name: 'AddUser',
  data() {
    return {
      showForm: true,
      user: {},
      setUpdateButton: false,
      requiredList: [],
    };
  },
  methods: {
    addUser() {
      this.$emit('userAddition', this.user);
    },
    updateUser() {
      this.$emit('update', this.user);
    },
    cancelSelected() {
      this.$emit('closePage', this.cancel);
    },
  },
  mounted() {
    if (this.userData != null) {
      this.user = this.userData;
      this.setUpdateButton = true;
    }
  },
  props: [
    'userData',
  ],
};
</script>

<style scoped>
.form_wrapper {
    background: rgba(0,0,0,0.7);
    position: absolute;
    top: 0;
    right: 0;
    left: 0;
    bottom: 0;
    display: flex;
    justify-content: center;
    align-items: center;
}

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
    margin: 60px 2px 4px;
    font-weight: bold;
}
#cancel {
    background: white;
    border-top-right-radius: 3px ;
    cursor: pointer;
    color: rgba(0,0,0,0.3);
    border: none;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    font-weight: bold;
}

#updateMember {
    background-color: #7a28c7;
    border-top-right-radius: 3px ;
    cursor: pointer;
    color: white;
    border: none;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    margin: 4px 2px;
    font-weight: bold;
    margin: 50px 100px 4px;
}

form {
    background-color: white;
    min-width: 60vw;
    min-height: 55vh;
    padding: 2rem 4rem 4rem;
    border-radius: 0.4rem;
}

.topContainer {
    display: flex;
    align-items: center;
    justify-content: center;
}
.topright {
    padding-left: 30px;
    margin-top: 0px;
}
.email {
    text-align: left;
    max-width: 500px;
}
.access {
    text-align: left;
    max-width: 500px;
}

.caption {
    font-family: sans-serif;
    font-size: 78%;
    color: rgba(0,0,0,0.3);
}

hr {
    background: rgba(253,100,98,0.1);
    border-width: 0.5px;
}

.topleft {
    text-align: left;
    /* max-width: 450px; */
    margin-right: 150px;
}
.inviteCaption {
    max-width: 500px;
}
.headButtonUpdate {
    margin-bottom: 60px;
}
</style>

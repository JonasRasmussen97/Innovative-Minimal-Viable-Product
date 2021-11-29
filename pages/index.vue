<template>
    <div class="container">
        <div class="row">
            <div class="col p-3 text-center">
                <b-img src="../static/logo.png"></b-img> 
            </div>
        </div>
         <div class="row">
            <div class="col p-3 text-center">
                <p><b-input v-model="username" variant="dark" placeholder="Enter your username"></b-input></p>
                <p><b-input v-model="password" type="password" variant="dark" placeholder="Enter your password"></b-input></p>
                <b-button variant="dark" @click="login(); $bvToast.show('login-toast')">Login</b-button>
            </div>
        </div>

          <div class="row">
            <div class="col p-3 text-center">
            {{this.status}}
            </div>
        </div>

    </div>



</template>


<script>
export default {
    methods: {
      login() {
          if(this.users.some(user => user.username === this.username && user.password === this.password)) {
              this.status = 'Logged in!';
              setTimeout(() => {
                this.$router.push('/marketplace');
              }, 2000);
          } else {
              this.status = 'Incorrect username or password!';
          }
      }  
    },
    data() {
        return {
            username: '',
            password: '',
            status: '',
            users: [
                {
                    username: 'Admin',
                    password: 'Admin'
                }
            ]
        }
    },
}
</script>

<style scoped>

</style>
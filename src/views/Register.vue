<template>
  <div>
    <div class = "container" align = center style = "padding-top: 20px">

        <h1> Register A New User </h1>
      <b-form style = "width: 50%" align = center>
        
        <b-input-group style = "margin-top: 35px" size = "lg" prepend="@" class="mb-2 mr-sm-2 mb-sm-0">
          <b-input v-model = "username"  placeholder="Username"></b-input>
        </b-input-group>

        <b-input-group style = "margin-top: 15px" size = "lg" prepend="@" class="mb-2 mr-sm-2 mb-sm-0">
          <b-input v-model = "password" type = "password"  placeholder="Password"></b-input>
        </b-input-group>

        <!-- <b-form-checkbox class="mb-2 mr-sm-2 mb-sm-0">Remember me</b-form-checkbox> -->

        <b-button size = "lg" @click = "submitRegisterButton" style = "margin-top: 15px">Register</b-button>
      </b-form>
    </div>
  </div>
</template>


<script>
import axios from "axios";

export default {
  name: "Register",
  components: {},
  data() {
    return {
      stories: [],
      username: null,
      password: null
    };
  },
  methods: {
    submitRegisterButton() {

      if (this.username.length == 0 || this.password.length == 0) {
        this.$swal('Invalid Length', 'Please input at least one character in each field', 'error')
        return;
      }

      
      axios
        .post("http://localhost:8080/register", {
          username: this.username,
          password: this.password
        })
        .then(() => {
          this.username = "";
          this.password = "";
          this.$swal('Registered', 'You have successfully registered', 'success')
          this.$router.push('/login')
        })
        .catch(() => {
          this.$swal('Invalid Registration', 'Username already exists', 'error')
          this.username = '';
          this.password = '';
        });
    }
  },
  computed: {
    //   validation() {
    //     //return this.userId.length > 4 && this.userId.length < 13
    //   }
  },
  created() {
    
  }
};
</script>

<style>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: Arial, Helvetica, sans-serif;
  line-height: 1.4;
  padding-bottom: 200px;
}
</style>
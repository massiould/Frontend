<template>
  <h1>Sign in</h1>
  <div class="form-container">
    <form name="login-form" @submit.prevent="login">
      <div class="mb-3">
        <label for="username">Username </label>
        <input type="text" id="username" v-model="input.username" class="form-input" />
      </div>
      <div>
        <label for="password">Password </label>
        <input type="password" id="password" v-model="input.password" class="form-input" />
      </div>
      <button type="submit">
        Se connecter
      </button>
    </form>
    <div class="output-message" v-if="output !== ''">
      <span>{{ output }}</span>
    </div>
  </div>
</template>

<script>
import { SET_AUTHENTICATION, SET_USERNAME } from "../store/storeconstants";
export default {
  name: 'LoginView',
  data() {
    return {
      input: {
        username: "",
        password: ""
      },
      output: "",
    }
  },
  methods: {
    login() {
      if (this.input.username != "" && this.input.password != "") {
        this.output = "Authentication complete";
        this.$store.commit(`auth/${SET_AUTHENTICATION}`, true);
        this.$store.commit(`auth/${SET_USERNAME}`, this.input.username);
        this.$router.push('/home');
      } else {
        this.$store.commit(`auth/${SET_AUTHENTICATION}`, false);
        this.output = "Username and password cannot be empty";
      }
    },
  },
}
</script>

<style scoped>
/* Style for form container *//* Style for form container */
.form-container {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  background-color: #fff;
  box-shadow: 0px 2px 10px rgba(0, 0, 0, 0.1);
}

/* Style for form labels */
label {
  display: block;
  margin-bottom: 5px;
  color: #333;
  text-align: left;
  font-size: 16px;
  font-weight: 500;
}

/* Style for form inputs */
input[type="text"],
input[type="password"] {
  width: calc(100% - 20px);
  padding: 12px;
  margin-bottom: 20px;
  border: 1px solid #ddd;
  border-radius: 3px;
}

/* Style for submit button */
button[type="submit"] {
  width: 100%;
  padding: 12px;
  border: none;
  border-radius: 3px;
  background-color: #0073b1; /* LinkedIn Blue */
  color: #fff;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s ease;
  font-size: 14px;
}

button[type="submit"]:hover {
  background-color: #005a8d; /* Darker Blue */
}

/* Style for output message */
.output-message {
  margin-top: 10px;
  font-weight: bold;
  color: #333;
}
</style>

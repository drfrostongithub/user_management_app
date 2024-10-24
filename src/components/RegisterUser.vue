<template>
  <div class="register-container">
    <h2>Register User</h2>
    <form @submit.prevent="registerUser" class="register-form">
      <input
        v-model="newUser.name"
        placeholder="Name"
        required
        class="form-input"
      />
      <input
        v-model="newUser.email"
        placeholder="Email"
        type="email"
        required
        class="form-input"
      />
      <select v-model="newUser.gender" required class="form-input">
        <option value="" disabled>Select Gender</option>
        <option value="male">Male</option>
        <option value="female">Female</option>
      </select>
      <select v-model="newUser.status" required class="form-input">
        <option value="" disabled>Select Status</option>
        <option value="active">Active</option>
        <option value="inactive">Inactive</option>
      </select>
      <button type="submit" class="register-button">Register</button>
    </form>
    <p v-if="successMessage" class="success-message">{{ successMessage }}</p>
    <p v-if="errorMessage" class="error-message">{{ errorMessage }}</p>
  </div>
</template>

<script>
  import axios from "axios";

  export default {
    data() {
      return {
        newUser: {
          name: "",
          email: "",
          gender: "",
          status: "",
        },
        successMessage: "",
        errorMessage: "",
      };
    },
    methods: {
      registerUser() {
        axios
          .post("https://gorest.co.in/public/v2/users", this.newUser)
          .then((response) => {
            if (response) {
              this.successMessage = "User registered successfully!";
              this.errorMessage = "";
              this.newUser = { name: "", email: "", gender: "", status: "" };
            }
          })
          .catch((error) => {
            if (
              error.response &&
              error.response.data &&
              error.response.data.message
            ) {
              this.errorMessage = "Error: " + error.response.data.message;
            } else {
              this.errorMessage = "Error: An unexpected error occurred.";
            }
            this.successMessage = "";
          });
      },
    },
  };
</script>

<style scoped>
  .register-container {
    max-width: 400px;
    margin: auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    background-color: #f9f9f9;
  }
  h2 {
    text-align: center;
    color: #333;
  }
  .register-form {
    display: flex;
    flex-direction: column;
  }
  .form-input {
    margin: 10px 0;
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  .register-button {
    padding: 10px;
    background-color: #28a745;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  .register-button:hover {
    background-color: #218838;
  }
  .success-message {
    color: #28a745;
    text-align: center;
  }
  .error-message {
    color: #dc3545;
    text-align: center;
  }
</style>

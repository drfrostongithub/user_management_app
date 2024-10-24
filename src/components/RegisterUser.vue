<template>
  <div>
    <h2>Register User</h2>
    <form @submit.prevent="registerUser">
      <input v-model="newUser.name" placeholder="Name" required />
      <input
        v-model="newUser.email"
        placeholder="Email"
        type="email"
        required
      />
      <select v-model="newUser.gender" required>
        <option value="" disabled>Select Gender</option>
        <option value="male">Male</option>
        <option value="female">Female</option>
      </select>
      <select v-model="newUser.status" required>
        <option value="" disabled>Select Status</option>
        <option value="active">Active</option>
        <option value="inactive">Inactive</option>
      </select>
      <button type="submit">Register</button>
    </form>
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
      };
    },
    methods: {
      registerUser() {
        axios
          .post("https://gorest.co.in/public/v2/users", this.newUser, {
            headers: {
              Authorization: "Bearer YOUR_ACCESS_TOKEN",
            },
          })
          .then(() => {
            alert("User registered successfully!");
            this.newUser = { name: "", email: "", gender: "", status: "" };
          })
          .catch((error) => {
            console.error("Error:", error.response);
          });
      },
    },
  };
</script>

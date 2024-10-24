<template>
  <div class="user-table">
    <h1>User Table</h1>

    <input v-model="searchQuery" placeholder="Search name" />

    <button @click="showModal = true">Add New User</button>

    <div v-if="showModal" class="modal">
      <div class="modal-content">
        <span class="close" @click="showModal = false">&times;</span>
        <h2>Add New User</h2>

        <div class="form-group">
          <label for="full_name">Full Name</label>
          <input
            id="full_name"
            v-model="newUser.full_name"
            placeholder="Full Name"
          />
        </div>
        <div class="form-group">
          <label for="gender">Gender</label>
          <input id="gender" v-model="newUser.gender" placeholder="Gender" />
        </div>
        <div class="form-group">
          <label for="age">Age</label>
          <input id="age" v-model="newUser.age" placeholder="Age" />
        </div>
        <div class="form-group">
          <label for="email">Email</label>
          <input id="email" v-model="newUser.email" placeholder="Email" />
        </div>
        <div class="form-group">
          <label for="phone">Phone Number</label>
          <input
            id="phone"
            v-model="newUser.phone_number"
            placeholder="Phone"
          />
        </div>
        <div class="form-group">
          <label for="address">Address</label>
          <input id="address" v-model="newUser.address" placeholder="Address" />
        </div>
        <div class="form-group">
          <label for="city">City</label>
          <input id="city" v-model="newUser.city" placeholder="City" />
        </div>
        <div class="form-group">
          <label for="country">Country</label>
          <input id="country" v-model="newUser.country" placeholder="Country" />
        </div>
        <div class="form-group">
          <label for="job_title">Job Title</label>
          <input
            id="job_title"
            v-model="newUser.job_title"
            placeholder="Job Title"
          />
        </div>

        <button @click="addUser">Add User</button>
      </div>
    </div>

    <table border="1">
      <thead>
        <tr>
          <th>No</th>
          <th>Full Name</th>
          <th>Gender</th>
          <th>Age</th>
          <th>Email</th>
          <th>Phone</th>
          <th>Address</th>
          <th>City</th>
          <th>Country</th>
          <th>Job Title</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(user, index) in filteredUsers" :key="user.id">
          <!-- <td v-if="user.editMode"><input v-model="user.id" /></td> -->
          <td>{{ user.id }}</td>

          <td v-if="user.editMode"><input v-model="user.full_name" /></td>
          <td v-else>{{ user.full_name }}</td>

          <td v-if="user.editMode"><input v-model="user.gender" /></td>
          <td v-else>{{ user.gender }}</td>

          <td v-if="user.editMode"><input v-model="user.age" /></td>
          <td v-else>{{ user.age }}</td>

          <td v-if="user.editMode"><input v-model="user.email" /></td>
          <td v-else>{{ user.email }}</td>

          <td v-if="user.editMode"><input v-model="user.phone_number" /></td>
          <td v-else>{{ user.phone_number }}</td>

          <td v-if="user.editMode"><input v-model="user.address" /></td>
          <td v-else>{{ user.address }}</td>

          <td v-if="user.editMode"><input v-model="user.city" /></td>
          <td v-else>{{ user.city }}</td>

          <td v-if="user.editMode"><input v-model="user.country" /></td>
          <td v-else>{{ user.country }}</td>

          <td v-if="user.editMode"><input v-model="user.job_title" /></td>
          <td v-else>{{ user.job_title }}</td>

          <td>
            <button v-if="!user.editMode" @click="editUser(user)">Edit</button>
            <button v-if="user.editMode" @click="saveUser(user)">Save</button>
            <button @click="deleteUser(index)">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
  import usersData from "../assets/MOCK_DATA.json";

  export default {
    data() {
      return {
        searchQuery: "",
        newUser: { full_name: "", email: "", job_title: "" },
        users: usersData,
        showModal: false,
      };
    },
    computed: {
      filteredUsers() {
        return this.users.filter((user) =>
          user.full_name.toLowerCase().includes(this.searchQuery.toLowerCase())
        );
      },
    },
    methods: {
      addUser() {
        if (
          this.newUser.full_name &&
          this.newUser.email &&
          this.newUser.job_title
        ) {
          this.users.push({
            id: this.users.length + 1,
            ...this.newUser,
            editMode: false,
          });
          this.newUser.full_name = "";
          this.newUser.email = "";
          this.newUser.job_title = "";
        }
        this.showModal = false;
      },
      editUser(user) {
        user.editMode = true;
      },
      saveUser(user) {
        user.editMode = false;
      },
      deleteUser(index) {
        this.users.splice(index, 1);
      },
    },
  };
</script>

<style scoped>
  .user-table {
    display: flex;
    flex-direction: column;
    flex-wrap: nowrap;
    align-items: center;
  }

  .modal {
    display: block;
    position: fixed;
    z-index: 1;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.4);
  }

  .modal-content {
    background-color: #fff;
    margin: auto auto;
    padding: 20px;
    border: 1px solid #888;
    width: 50%;
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

  .form-group {
    margin-bottom: 15px;
  }

  label {
    display: flex;
    margin-bottom: 5px;
  }

  input {
    padding: 8px;
    width: 100%;
    box-sizing: border-box;
  }

  button {
    padding: 10px 15px;
    margin-top: 10px;
  }
</style>

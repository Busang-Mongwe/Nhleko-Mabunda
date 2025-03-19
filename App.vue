<template>
  <div>
    <h1>User Management System</h1>

    <UserForm 
      :userData="currentUser" 
      :isEditing="isEditing" 
      @add-user="addUser"
      @update-user="updateUser"
    />
    
    <UserTable 
      :users="users" 
      @edit-user="editUser" 
      @delete-user="deleteUser"
    />
  </div>
</template>

<script>
import UserTable from "./components/UserTable.vue";
import UserForm from "./components/UserForm.vue";

export default {
  components: {
    UserTable,
    UserForm,
  },
  data() {
    return {
      users: [], // User list
      currentUser: null, // Store the user being edited
      isEditing: false,
    };
  },
  methods: {
    addUser(newUser) {
      newUser.id = Date.now(); // Assign a unique ID
      this.users.push(newUser); // Add user to list
    },
    editUser(user) {
      this.currentUser = user; // Set user for editing
      this.isEditing = true;
    },
    updateUser(updatedUser) {
      const index = this.users.findIndex((u) => u.id === updatedUser.id);
      if (index !== -1) {
        this.users[index] = updatedUser; // Update user
      }
      this.currentUser = null;
      this.isEditing = false;
    },
    deleteUser(userId) {
      this.users = this.users.filter((user) => user.id !== userId); // Remove user
    },
  },
};
</script>

<style>
h1{
  text-align: center;
}
</style>

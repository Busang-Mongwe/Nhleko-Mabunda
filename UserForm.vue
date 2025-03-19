<template>
  <div class="form-container">
    <h2>{{ isEditing ? "Edit User" : "Add User" }}</h2>
    <P>Name: 
      <input v-model="user.name" placeholder="Full Name" required/>
    </P>
    <p>Email:
      <input v-model="user.email" placeholder="Email Address" required/>
    </p>
    <p>Contact:
      <input v-model="user.contact" placeholder="Cellphone number" required>
    </p>
    <p>
      Occupation:
      <input v-model="user.role" placeholder="Role" required>
    </p>
    <button @click="saveUser">{{ isEditing ? "Update" : "Add" }} User</button>
  </div>
</template>

<script>
export default {
  props: {
    userData: Object, // Received from App.vue when editing
    isEditing: Boolean,
  },
  data() {
    return {
      user: { id: null, name: "", email: "", contact: "" ,role: "" },
    };
  },
  watch: {
    userData: {
      immediate: true,
      handler(newValue) {
        this.user = newValue ? { ...newValue } : { id: null, name: "", email: "",contact: "" ,role: "" };
      },
    },
  },
  methods: {
    saveUser() {
      if (this.user.name && this.user.email && this.user.contact && this.user.role) {
        this.$emit(this.isEditing ? "update-user" : "add-user", { ...this.user });
        this.user = { id: null, name: "", email: "", contact: "", role: "" }; // Reset form
      } else {
        alert("Please fill in all fields!");
      }
    },
  },
};
</script>

<style scoped>
.form-container {
  /*margin-bottom: 20px;*/
  border: solid 1px #ddd;
  width: 80%;
  padding: 20px;
  background-color: blanchedalmond;
  margin: auto;
}
input {
  display: block;
  margin: 5px 0;
  padding: 8px;
  width: 96%;
}
button {
  background-color:green;
  color: white;
  padding: 10px;
  border-radius: 4px;
  cursor: pointer;
}
button:hover{
  background-color: lightgreen;
  color: black;
}
</style>

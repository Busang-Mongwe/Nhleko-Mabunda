<template>
    
    <div ref="tableContainer" class="tableContainer">
      <h1>User List</h1>
      <table>
        <thead>
          <tr>
            <th>Name</th>
            <th>Email</th>
            <th>Contact</th>
            <th>Occupation</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in users" :key="user.id">
            <td>{{ user.name }}</td>
            <td>{{ user.email }}</td>
            <td>{{ user.contact }}</td>
            <td>{{ user.role }}</td>
            <td>
              <button class="edit" @click="$emit('edit-user', user)">Edit</button>
              <button class="delete" @click="$emit('delete-user', user.id)">Delete</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <button class="download-btn" @click="downloadTable">Download</button>
  </template>
  
  <script>
import html2pdf from "html2pdf.js";

export default {
  props: {
    users: Array, // Receive users list from parent
  },
  methods: {
    downloadTable() {
      const element = this.$refs.tableContainer;
      html2pdf().from(element).save("User_List_Document.pdf");
    },
  },
};
</script>
  
  
  <style scoped>
  .tableContainer{
    margin-top: 20px;
  }
  table {
    width: 85%;
    border-collapse: collapse;
    margin: auto;
    
  }
  h2{
    text-align: center;
    margin-top: 20px;
  }
  th, td {
    padding: 6px;
    border: 2px solid #ddd;
    text-align: left;
  }
  button {
    margin: 5px;
    padding: 10px;
    border: solid 1px #ddd;
    border-radius: 4px;
    width: 70px;
    cursor: pointer;
  }
  .download-btn{
    margin: 10px 0 0 8%;
    padding: 10px;
    color: white;
    background-color: green;
    width: 90px;
  }
  .download-bnt:hover{
    background-color: lightgreen;
    color: black;
  }
  .edit {
    background-color: green;
    color: white;
  }
  .edit:hover {
    background-color: lightgreen;
    color: black;
  }
  .delete {
    background-color: red;
    color: white;
  }
  .delete:hover{
    background-color: rgb(221, 96, 96);
    color: black;
  }

  </style>
  
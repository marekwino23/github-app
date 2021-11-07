<template>
<div class="header">
  <h1>Git Hub App</h1>
  <img class="github" src="./assets/github-icon-38980.png"/>
  <FontAwesomeIcon icon='user-secret'/>
  </div>
  <div class="field">
  <input type="text" placeholder="Filter By Name" v-model="word">
  </div>
<div>
  <table>
    <th>id</th>
    <th>name</th>
    <th>photo</th>
  <tr v-for="contact in filterContacts" :key="contact.id">
    <td>{{contact.id}}</td>
    <td>{{contact.login}}</td> 
    <td><img class="icon" :src="contact.avatar_url"></td>
  </tr>
  </table>
</div>
</template>

<script>


export default {
  name: 'App',
  data: function(){
    return{
      contacts: [],
      type:"",
      word:""
    }
},

computed:{
  filterContacts: function(){
       return this.contacts.filter((contact)=>{
        return contact.login.toLowerCase().match(this.word.toLowerCase())
      })
  }
},
mounted(){
  fetch('https://api.github.com/users', {
  method: 'GET', 
  headers: {
    'Content-Type': 'application/json',
  },
})
.then(response => response.json())
.then(data => {
  this.contacts = data
})
.catch((error) => {
  console.error('Error:', error);
})}
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: aliceblue;
  color: #2c3e50;
  margin: 0 auto;
}

.github {
    width: 6%;
    margin-left: 1%;
}

.header{
  display: flex;
  justify-content: center;
}

.icon{
  width: 100%;
  height: auto;
}

h1:hover{
  color:rgb(41, 142, 182)
}

.github:hover{
  transform: scale(1.2);
}


@media only screen and (max-width: 600px) {
  .github {
    width: 30%;
  }
  .header {
    display: flex;
    justify-content: space-evenly;
    margin: 0px 0px 4px 32px;
}
}

table {
    font-family: Arial, Helvetica, sans-serif;
    border-collapse: collapse;
    width: 50%;
    margin-left: 25%;
    margin-top: 4%;
}

table td, table th {
  border: 1px solid #ddd;
  padding: 8px;
}

table tr:nth-child(even){background-color: #f2f2f2;}

table tr:hover {background-color: #ddd;}

table th {
  padding-top: 12px;
  padding-bottom: 12px;
  text-align: center;
  font-weight: bold;
  background-color: #2278db;
  color: white;
}

table th:hover{
  background-color: rgb(42, 156, 201);
}


input[type=text] {
    width: 36%;
    padding: 12px 20px;
    margin: 31px 0px 0px 0px;
    display: inline-block;
    border: 1px solid #ccc;
    border-radius: 20px;
    box-sizing: border-box;
}

li{
  list-style-type:none;
}
</style>

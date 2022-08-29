<script>

import { useUserStore } from './stores/users';
import { ref } from 'vue'

const user_store = useUserStore()

const user_input = ref({
  name: '',
  lname: '',
  email: '',
  gender: '',
  age: '',
  message: ''
})

const sort = ref(false)

const CreateUser = () => {
  if (
    !user_input.value.name ||
    !user_input.value.email ||
    !user_input.value.lname ||
    !user_input.value.gender ||
    !user_input.value.age
  ) {
    return alert('Please enter all fields and select gender and age')
  }

  user_store.create(user_input.value)

  user_input.value = {
    name: '',
    lname: '',
    email: '',
    gender: '',
    age: '',
    message: ''
  }
}

</script>

<template>
<h1>Team manager</h1>

<form @submit.prevent="CreateUser">
  <div class="form-container">
    <div class='first container'>
      <p>Enter personal details:</p>

      <input class="field" type="text" placeholder="Enter first name" v-model="user_input.name"><br>
      <input class="field" type="text" placeholder="Enter last name" v-model="user_input.lname"><br>
      <input class="field" type="email" placeholder="Enter email" v-model="user_input.email">
      <p>Select your gender:</p>

      <select v-model="user_input.gender">
        <option disabled value="">please select one</option>
        <option>male</option>
        <option>female</option>
        <option>other</option>
      </select>
    </div>
    <div class='second container'>


      <p>Select your age group:</p>
      <div class="select-radio">
        <input class="radio" type="radio" id="one" value="18-25" v-model="user_input.age" />
        <label for="one"> 18-25</label><br>

        <input class="radio" type="radio" id="two" value="older than 25" v-model="user_input.age" />
        <label for="two"> Older than 25</label><br />
      </div>
      <p>Add comment (optional):</p>

      <textarea v-model="user_input.message"></textarea>
    </div>
  </div>
  <input class="add-button" type="submit" value="ADD USER">

</form>

</template>

<style scoped>
    main {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
    
    form {
      border: 2px solid #385170;
      border-radius: 10px;
      align-items: center;
      justify-content: center;
      text-align: center;
      padding: 30px 0px;
      margin: auto;
      width: 800px;
    }
    
    .form-container {
      display: flex;
      align-items: center;
      justify-content: center;
    
    }
    
    .container {
      margin: 0px 70px;
    }
    
    .select-radio {
      text-align: left;
    }
    
    input {
      margin-bottom: 10px;
    }
    
    .field,
    select,
    .radio,
    textarea {
      border: 2px solid #385170;
      border-radius: 10px;
      padding: 10px;
    }
    
    .field,
    textarea {
      width: 250px;
    }
    
    textarea {
      height: 70px;
    }
    
    select {
      width: 270px;
    
    }
    
    .add-button {
      margin-top: 30px;
    }
    
    .add-button {
      background: #d8e5f8;
      border: 2px solid #385170;
      border-radius: 20px;
      padding: 5px 10px;
      color: #385170;
      transition: 0.5s;
    }
    
    .add-button:hover {
      background: #385170;
      border: 2px solid #d8e5f8;
      color: #d8e5f8;
    }
    
    h1,
    h2 {
      text-align: center;
      color: #385170;
    }
    
    </style>
    
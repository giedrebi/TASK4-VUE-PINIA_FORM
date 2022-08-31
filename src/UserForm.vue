<script setup>
import { useUserStore } from './stores/users';
import { ref } from 'vue'

const user_store = useUserStore()
const user_input = ref({
  name: '',
  lname: '',
  email: '',
  gender: '',
  age: '',
  comment: ''
})

const errors = ref({
  firstNameError: false,
  lastNameError: false,
  nameMessage: false,
  lastNameMessage: false,
  emailError: false,
  genderError: false,
  ageError: false
})

const CreateUser = () => {
  errors.value.firstNameError = !user_input.value.name || user_input.value.name.length <= 3
  errors.value.lastNameError = !user_input.value.lname || user_input.value.lname.length <= 3
  errors.value.nameMessage = user_input.value.name.length <= 3
  errors.value.lastNameMessage = user_input.value.lname.length <= 3
  errors.value.emailError = !user_input.value.email
  errors.value.genderError = !user_input.value.gender
  errors.value.ageError = !user_input.value.age

  console.log(Object.values(errors.value))
  if (Object.values(errors.value).some(value => value)) {
    return
  }

  else {
    return user_store.create(user_input.value),
      user_input.value = {
        name: '',
        lname: '',
        email: '',
        gender: '',
        age: '',
        comment: ''
      },
      errors.value = {
        firstNameError: false,
        lastNameError: false,
        nameMessage: false,
        lastNameMessage: false,
        emailError: false,
        genderError: false,
        ageError: false
      }
  }
}

</script>
  
  <template>
  <h1>Team manager</h1>

  <form @submit.prevent="CreateUser">
    <div class="form-container">
      <div class='first container'>
        <p>Enter personal details:</p>

        <input class="field" id="fname" type="text" placeholder="Enter first name" v-model="user_input.name"
          :class="{ error: errors.firstNameError }"><br />
        <p class="message" :class="{ errorMessage: errors.nameMessage }">Please enter more than 3 characters</p>

        <input class="field" id="lname" type="text" placeholder="Enter last name" v-model="user_input.lname"
          :class="{ error: errors.lastNameError }"><br>
        <p class="message" :class="{ errorMessage: errors.lastNameMessage }">Please enter more than 3 characters</p>

        <input class="field" type="email" id="email" placeholder="Enter email" v-model="user_input.email"
          :class="{ error: errors.emailError }">
        <p>Select your gender:</p>

        <select v-model="user_input.gender" id="gender" :class="{ error: errors.genderError }">
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
          <label for="one" class="radio-label" :class="{ errorRadio: errors.ageError }"> 18-25</label><br>

          <input class="radio" type="radio" id="two" value="older than 25" v-model="user_input.age" />
          <label for="two" class="radio-label" :class="{ errorRadio: errors.ageError }"> Older than 25</label><br />
        </div>

        <p>Add comment (optional):</p>

        <textarea v-model="user_input.comment"></textarea>
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

/* ERRORS */

.message {
  display: none;
}

.errorMessage {
  display: block;
  font-size: xx-small;
  margin-top: -10px;
}

.error {
  border: solid 2px red !important;
}

.errorRadio {
  color: red !important;
}
</style>
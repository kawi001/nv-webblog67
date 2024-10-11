<template>
  <div class="register-container">
    <h1>Register</h1>
    <form @submit.prevent="createUser" class="register-form">
      <div class="form-group">
        <label for="name">Name:</label>
        <input type="text" id="name" v-model="user.name" required />
      </div>
      <div class="form-group">
        <label for="lastname">Last Name:</label>
        <input type="text" id="lastname" v-model="user.lastname" required />
      </div>
      <div class="form-group">
        <label for="email">Email:</label>
        <input type="email" id="email" v-model="user.email" required />
      </div>
      <div class="form-group">
        <label for="password">Password:</label>
        <input type="password" id="password" v-model="user.password" required />
      </div>
      <div class="form-group">
        <button type="submit" class="submit-button">Create User</button>
      </div>
    </form>
  </div>
</template>

<script>
import UsersService from '../../services/UsersService';
export default {
  data() {
    return {
      user: {
        name: '',
        lastname: '',
        email: '',
        password: '',
        status: 'active'
      }
    };
  },
  methods: {
    async createUser() {
      try {
        await UsersService.post(this.user);
        this.$router.push('/users');
      } catch (err) {
        console.log(err);
      }
    }
  }
}
</script>

<style scoped>
.register-container {
  max-width: 400px;
  margin: 0 auto;
  padding: 40px;
  border: 1px solid #333;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  background-color: #000; /* Black background */
  color: #ffcc00; /* Yellow text */
}

h1 {
  text-align: center;
  color: #ffcc00; /* Yellow */
  font-size: 24px; /* Increased font size */
}

.register-form {
  display: flex;
  flex-direction: column;
}

.form-group {
  margin-bottom: 15px;
}

label {
  font-weight: bold;
  color: #ffcc00; /* Yellow text */
  font-size: 16px; /* Increased font size */
}

input {
  padding: 10px;
  border: 1px solid #ffcc00; /* Yellow border */
  border-radius: 4px;
  outline: none;
  transition: border-color 0.3s;
  color: #fff; /* White text for input fields */
  background-color: #333; /* Dark background for input fields */
  font-size: 16px; /* Increased font size */
}

input:focus {
  border-color: #ffcc00; /* Yellow focus color */
}

.submit-button {
  background-color: #ffcc00; /* Yellow */
  color: #333; /* Dark text */
  padding: 10px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-size: 18px; /* Increased font size */
  transition: background-color 0.3s;
}

.submit-button:hover {
  background-color: #e6b800; /* Darker yellow on hover */
}
</style>

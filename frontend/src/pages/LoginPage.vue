<template>
  <v-container class="login-page" fluid>
    <v-row justify="center" align="center" class="fill-height">
      <v-col cols="12" sm="8" md="4" lg="3">
        <v-card class="pa-6" elevation=".1" rounded="xl">
          <v-card-title class="text-h5 font-weight-bold text-center mb-4">
            <div class="text-center">
              <span class="text-h1">👋</span>
              <br />
              <span class="text-h5">Welcome To TMS</span>
            </div>
          </v-card-title>

          <v-card-subtitle class="text-center mb-6 text-grey-darken-1">
            Please login to your account
          </v-card-subtitle>

          <v-form @submit.prevent="handleLogin">
            <v-text-field
              v-model="form.username"
              label="Username"
              prepend-inner-icon="mdi-account"
              variant="outlined"
              color="primary"
              density="comfortable"
              required
            />

            <v-text-field
              v-model="form.password"
              label="Password"
              type="password"
              prepend-inner-icon="mdi-lock"
              variant="outlined"
              color="primary"
              density="comfortable"
              required
            />

            <v-btn
              type="submit"
              color="primary"
              class="mt-4"
              block
              size="large"
              rounded="xl"
            >
              Login
            </v-btn>

            <div class="text-center mt-4">
              <span>Don't have an account?</span>
              <RouterLink to="/register" class="text-primary font-weight-bold ml-1">
                Register
              </RouterLink>
            </div>
          </v-form>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import { ref } from 'vue'
import axios from 'axios'
import { useRouter } from 'vue-router'

const form = ref({
  username: '',
  password: '',
})

const router = useRouter()

const handleLogin = async () => {
  try {
    const response = await axios.post('http://localhost:5000/api/auth/login', {
      username: form.value.username,
      password: form.value.password,
    })
    console.log(response.data)
    localStorage.setItem('token', response.data.token);

    router.push('/tasks') 
  } catch (error) {
    console.error('Login failed:', error)
    alert('Login failed. Please check your credentials.')
  }
}

</script>

<style scoped>
.login-page {
  min-height: 100vh;
  background-color: #f5f7fa;
  padding: 20px;
  background-image: url('https://png.pngtree.com/thumb_back/fh260/background/20240209/pngtree-task-management-business-planning-app-illustration-vector-image_15623958.jpg');
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
}

@media (max-width: 600px) {
  .login-page {
    padding: 10px;
  }
}
</style>

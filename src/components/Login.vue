<template>
  <div>
    <!-- <v-img
      class="mx-auto my-6"
      max-width="100"
      src="@/assets/NULLTV_logo.svg"
    ></v-img> -->

    <v-card
      class="mx-auto pa-12 pb-8"
      elevation="8"
      max-width="448"
      rounded="lg"
    >

      <div v-if="is_register">
        <div class="text-subtitle-1 text-medium-emphasis">Account</div>
        <v-text-field
          density="compact"
          placeholder="Email address"
          prepend-inner-icon="mdi-email-outline"
          variant="outlined"
          v-model="email"
          :rules="[rules.required, rules.email]"
        ></v-text-field>

        <div class="text-subtitle-1 text-medium-emphasis d-flex align-center justify-space-between">
          Password
          <a
            class="text-caption text-decoration-none text-blue"
            href="#"
            rel="noopener noreferrer"
            target="_blank"
          >
            Forgot password?</a>
        </div>
        <v-text-field
          :append-inner-icon="visible ? 'mdi-eye-off' : 'mdi-eye'"
          :type="password_visible ? 'text' : 'password'"
          density="compact"
          placeholder="Enter your password"
          prepend-inner-icon="mdi-lock-outline"
          variant="outlined"
          @click:append-inner="password_visible = !password_visible"
          v-model="password"
          :rules="[rules.required]"
        ></v-text-field>


        <v-card
          class="mb-12"
          color="surface-variant"
          variant="tonal"
        >
          <v-card-text class="text-medium-emphasis text-caption">
            Warning: After 3 consecutive failed login attempts, you account will be temporarily locked for three hours. If you must login now, you can also click "Forgot login password?" below to reset the login password.
          </v-card-text>
        </v-card>

        <v-btn
          block
          class="mb-8"
          color="blue"
          size="large"
          variant="tonal"
          @click="login({email: email, password: password})"
        >
          Log In
        </v-btn>

        <v-card-text class="text-center">
          <a
            class="text-blue text-decoration-none"
            rel="noopener noreferrer"
            target="_blank"
          >
            <v-btn variant="text" :ripple="false"
              @click="is_register = !is_register"
            >Sign up now 
              <v-icon icon="mdi-chevron-right"></v-icon>
            </v-btn>
          </a>
        </v-card-text>
      </div>
    
      
      <div v-if="!is_register">
        <div class="text-subtitle-1 text-medium-emphasis">Username</div>
        <v-text-field
          density="compact"
          placeholder="User name"
          prepend-inner-icon="mdi-email-outline"
          variant="outlined"
          v-model="username"
          :rules="[rules.required]"
        ></v-text-field>

        <div class="text-subtitle-1 text-medium-emphasis">Account</div>
        <v-text-field
          density="compact"
          placeholder="Email address"
          prepend-inner-icon="mdi-email-outline"
          variant="outlined"
          v-model="email"
          :rules="[rules.required, rules.email]"
        ></v-text-field>

        <div class="text-subtitle-1 text-medium-emphasis">Password</div>
          <v-text-field
            :append-inner-icon="visible ? 'mdi-eye-off' : 'mdi-eye'"
            :type="password_visible ? 'text' : 'password'"
            density="compact"
            placeholder="Enter your password"
            prepend-inner-icon="mdi-lock-outline"
            variant="outlined"
            @click:append-inner="password_visible = !password_visible"
            v-model="password"
            :rules="[rules.required]"
        ></v-text-field>

        <div class="text-subtitle-1 text-medium-emphasis">Password Again</div>
          <v-text-field
            :append-inner-icon="visible ? 'mdi-eye-off' : 'mdi-eye'"
            :type="password_visible ? 'text' : 'password'"
            density="compact"
            placeholder="Enter your password again"
            prepend-inner-icon="mdi-lock-outline"
            variant="outlined"
            @click:append-inner="password_visible = !password_visible"
            v-model="password_again"
            :rules="[rules.required]"
        ></v-text-field>

        <v-btn
          block
          class="mb-8"
          color="blue"
          size="large"
          variant="tonal"
          @click="register({username: username, email: email, password: password})"
        >
          Sign Up
        </v-btn>

        <v-btn variant="text" :ripple="false"
          @click="is_register = !is_register"
        >
          back to login 
          <v-icon icon="mdi-chevron-right"></v-icon>
        </v-btn>

      </div>

    </v-card>

  </div>
</template>

<script setup>
import { ref } from 'vue'

const username = ref(null)
const email = ref(null)
const password = ref(null)
const password_again = ref(null)

const password_visible = ref(false)

const is_register = ref(true)

const rules = {
  required: value => !!value || 'Required.',
  counter: value => value.length <= 20 || 'Max 20 characters',
  email: value => {
    const pattern = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
    return pattern.test(value) || 'Invalid e-mail.'
  },
}

function login(value) {
  console.log(value)
  fetch(`127.0.0.1:8888/user/login`, {
      headers: {
          'Content-Type': 'application/json; charset=UTF-8',
      },
      method: 'POST',
      credentials: 'include',
      body: JSON.stringify(value)
  })
  .then(response => response.json())
  .then(json => {
      if (json.status === 200) {
          const user = json.data
          // 保存用户信息
          this.$store.commit('setUserInfo', user)
          // 跳转到首页
          this.$router.push('/')
      } else {
          this.message = json.message
          this.showMessage = true
      }
  })
  .catch(e => {
      return null
  })
}


function register(value) {
  console.log(value)
  fetch(`/user/register`, {
      headers: {
          'Content-Type': 'application/json; charset=UTF-8',
      },
      method: 'POST',
      credentials: 'include',
      body: JSON.stringify(value)
  })
  .then(response => response.json())
  .then(json => {
      if (json.status === 200) {
          const user = json.data
          // 保存用户信息
          this.$store.commit('setUserInfo', user)
          // 跳转到首页
          this.$router.push('/')
      } else {
          this.message = json.message
          this.showMessage = true
      }
  })
  .catch(e => {
      return null
  })
}


</script>
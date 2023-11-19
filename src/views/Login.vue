<template>
  <v-app>
    <v-main>
      <v-container>
        <v-row>
          <v-col cols="12" md="6" offset-md="3">
            <v-card>
              <v-card-title>
                <span class="headline">Login</span>
              </v-card-title>
              <v-card-text>
                <v-form>
                  <v-text-field
                    v-model="email"
                    label="Email"
                    type="email"
                  >
                  </v-text-field>
                  <v-text-field
                    v-model="password"
                    label="Password"
                    type="password"
                  >
                  </v-text-field>
                </v-form>
                </v-card-text>
                <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn 
                  color="primary"
                  @click="login({email: email, password: password})"
                >
                  Login
                </v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>


<script setup>
import { ref } from 'vue'

const email = ref(null)
const password = ref(null)

// function login(value) {
//     fetch(`/user/login`, {
//         headers: {
//             'Content-Type': 'application/json; charset=UTF-8',
//             'X-XSRF-TOKEN': this.$cookies.get('XSRF-TOKEN')
//         },
//         method: 'POST',
//         credentials: 'include',
//         body: JSON.stringify(value)
//     })
//     .then(response => response.json())
//     .then(json => {
//         if (json.status === 200) {
//             const user = json.data
//             // 保存用户信息
//             this.$store.commit('setUserInfo', user)
//             // 跳转到首页
//             this.$router.push('/')
//         } else {
//             this.message = json.message
//             this.showMessage = true
//         }
//     })
//     .catch(e => {
//         return null
//     })
// }



</script>
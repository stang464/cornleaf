<template>
  <v-app>
    <v-row align="center" justify="center">
      <v-card>
        <v-col cols="12">
          <v-card-title>เข้าสู่ระบบ</v-card-title>
        </v-col>
        <v-col cols="12">
          <v-form ref="form">
            <v-text-field
              v-model="email"
              placeholder="Email"
              type="email"
              solo
              rounded
              @keyup.enter.native="submit"
            ></v-text-field>
            <v-text-field
              v-model="password"
              placeholder="Password"
              type="password"
              solo
              rounded
              @keyup.enter.native="submit"
            ></v-text-field>
            <v-btn color="primary" @click="submit">login</v-btn>
          </v-form>
        </v-col>
      </v-card>
    </v-row>
  </v-app>
</template>

<script>
import firebase from '~/plugins/firebaseConfig'
export default {
  data() {
    return {
      email: '',
      password: ''
    }
  },

  methods: {
    submit() {
      if (this.email === '') {
        alert('กรุณากรอก EMAIL')
      } else if (this.password === '') {
        alert('กรุณากรอกรหัสผ่าน')
      } else {
        const auth = firebase.auth()
        auth
          .signInWithEmailAndPassword(this.email, this.password)
          .then(() => {
            this.$store.commit('setLogined', true)
            this.$router.replace('/dashbord')
          })
          .catch((err) => {
            alert(err)
          })
      }
    }
  }
}
</script>

<style lang="postcss" scoped>
@import url('https://fonts.googleapis.com/css2?family=Prompt&display=swap');
.theme--light.v-application {
  background: #001040;
  color: #ffffff;
}
.v-application {
  font-family: 'Prompt', sans-serif;
}
</style>

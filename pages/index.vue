<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card>
        <v-card-title class="headline"> Quem é você? </v-card-title>
        <v-form v-model="valid">
          <v-container>
            <v-row>
              <v-col cols="12" md="12">
                <v-text-field
                  v-model="email"
                  :rules="emailRules"
                  label="E-mail"
                  required
                ></v-text-field>
              </v-col>
              <v-col cols="12" md="12">
                <v-text-field
                  class="mb-3"
                  v-model="password"
                  :append-icon="show1 ? 'mdi-eye' : 'mdi-eye-off'"
                  :rules="[rules.required, rules.min]"
                  :type="show1 ? 'text' : 'password'"
                  name="input-10-1"
                  label="Senha"
                  hint="At least 8 characters"
                  counter
                  @click:append="show1 = !show1"
                ></v-text-field>
              </v-col>
            </v-row>
            <v-btn
              color="primary"
              @click="onLogin"
              :disabled="!valid"
              elevation="2"
              >Entrar</v-btn
            >
          </v-container>
        </v-form>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data() {
    return {
      show1: false,
      valid: false,
      password: '',
      email: '',
      welcomeMsg: '',
      rules: {
        required: (value) => !!value || 'Digite uma senha!.',
        min: (v) => v.length >= 8 || 'Minimo 8 characters',
        emailMatch: () => `O e-mail existe mas a senha está incorreta`,
      },
      emailRules: [
        (v) => !!v || 'Digite um e-mail!',
        (v) => /.+@.+/.test(v) || 'Isso não é um e-mail!',
      ],
    }
  },
  methods: {
    onLogin() {
      window.localStorage.setItem(
        'email',
        this.email
      )
      window.localStorage.setItem(
        'password',
        this.password
      )
      window.sessionStorage.setItem('isLogged', true);
      this.$router.push({path: '/home'});
    },
  },
}
</script>

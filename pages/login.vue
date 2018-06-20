<template>
  <!-- <v-card class="elevation-12">
    <v-toolbar dark color="primary">
      <v-toolbar-title>ログイン</v-toolbar-title>
      <v-spacer></v-spacer>
    </v-toolbar>
    <v-card-text>
      <v-form>
        <v-text-field prepend-icon="person" name="email" label="email" type="email"></v-text-field>
        <v-text-field id="password" prepend-icon="lock" name="password" label="Password" type="password"></v-text-field>
      </v-form>
    </v-card-text>
    <v-card-actions>
      <v-chip left>
        <span>Or</span>
      </v-chip>
      <div v-for="s in strategies" :key="s.key" class="mb-2">
        <v-btn @click="$auth.loginWith(s.key)" block :style="{background: s.color}" class="login-button">Login with {{ s.name }}</v-btn>
      </div>
      <v-spacer></v-spacer>
      <v-btn color="primary">Login</v-btn>
    </v-card-actions>
  </v-card> -->
  <div class="container d-flex align-items-center justify-content-center flex-column">
    <v-progress-circular :size="70" :width="7" indeterminate color="green"></v-progress-circular>
    Logging in...
  </div>
</template>

<style scoped>
.container {
  min-height: 70vh;
}
.login-button {
  border: 0;
};
</style>

<script>
import busyOverlay from '~/components/busy-overlay'

export default {
  layout: 'center',
  middleware: ['auth'],
  components: { busyOverlay },
  mounted () {
    this.$auth.loginWith('google')
  },
  data () {
    return {
      username: '',
      password: '123',
      error: null
    }
  },
  computed: {
    strategies: () => ([
      // { key: 'auth0', name: 'Auth0', color: '#ec5425' },
      { key: 'google', name: 'Google', color: '#4284f4' }
      // { key: 'facebook', name: 'Facebook', color: '#3c65c4' },
      // { key: 'github', name: 'Github', color: '#202326' }
    ]),
    redirect () {
      return (
        this.$route.query.redirect &&
        decodeURIComponent(this.$route.query.redirect)
      )
    },
    isCallback () {
      return Boolean(this.$route.query.callback)
    }
  },
  methods: {
    async login () {
      this.error = null

      return this.$auth
        .loginWith('local', {
          data: {
            username: this.username,
            password: this.password
          }
        })
        .catch(e => {
          this.error = e + ''
        })
    }
  }
}
</script>

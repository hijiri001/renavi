<template>
  <div class="text-xs-center">
    <v-menu
      v-if="user"
      :close-on-content-click="false"
      :nudge-width="200"
      v-model="menu"
      offset-x
    >
      <v-btn
        slot="activator"
        icon
        @click.stop="handleMenu()"
      >
        <v-avatar size="42">
          <img :src="user.picture" >
        </v-avatar>
      </v-btn>
      <v-card>
        <v-list>
          <v-list-tile avatar>
            <v-list-tile-avatar>
              <img :src="user.picture" :alt="user.given_name">
            </v-list-tile-avatar>
            <v-list-tile-content>
              <v-list-tile-title>{{`${user.given_name} ${user.family_name}`}}</v-list-tile-title>
              <v-list-tile-sub-title>{{user.email}}</v-list-tile-sub-title>
            </v-list-tile-content>
          </v-list-tile>
        </v-list>
        <v-divider></v-divider>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn outline flat @click="logout">ログアウト</v-btn>
        </v-card-actions>
      </v-card>
    </v-menu>
    <v-btn
      v-else
      icon
      @click.stop="handleMenu()"
    >
      <v-icon>apps</v-icon>
    </v-btn>
  </div>
</template>

<script>
export default {
  // props: ['menu'],
  data () {
    return {
      menu: false
    }
  },
  computed: {
    user () {
      return this.$auth.$state.user
    }
  },
  methods: {
    handleMenu () {
      if (this.user) {
        this.menu = !this.menu
      } else {
        this.$router.replace('/login')
      }
    },
    async logout () {
      await this.$auth.logout()
      this.menu = false
    }
  }
}
</script>

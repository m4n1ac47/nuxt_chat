
<template>
<v-app>
  <v-navigation-drawer app v-model="drawer" mobile-break-point="650">
    <v-list subheader>
      <v-subheader>Список людей в комнате</v-subheader>

      <v-list-item v-for="item in users" :key="item.id" @click.prevent>

        <v-list-item-content>
          <v-list-item-title>{{ item.name }}</v-list-item-title>
        </v-list-item-content>

        <v-list-item-icon>
          <v-icon :color="item.id === 2 ? 'primary' : 'grey'">mdi-comment</v-icon>
        </v-list-item-icon>
      </v-list-item>
    </v-list>
  </v-navigation-drawer>
  <v-app-bar app>
    <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
    <v-btn icon @click="exit">
      <v-icon>mdi-arrow-left</v-icon>
    </v-btn>
    <v-toolbar-title>Чат комнаты {{ user.room }}</v-toolbar-title>
  </v-app-bar>
  <v-content>
    <div style="height: 100%">
      <nuxt/>
    </div>
  </v-content>
  </v-app>
</template>

<script>
import { mapState, mapMutations } from 'vuex'

export default {
  data: () => ({
    drawer: true,
    users: [
      { id: 1, name: 'User 1'},
      { id: 2, name: 'User 2'},
    ]
  }),
  computed: {
    ...mapState(['user'])
  },
  methods: {
    ...mapMutations(['clearData']),

    exit() {
      this.$router.push('/?message=leftChat')
      this.clearData()
    }
  }
}
</script>

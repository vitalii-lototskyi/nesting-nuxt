<template>
  <v-layout column>
    <v-flex xs12 sm6 offset-sm3>
      <v-subheader v-text="subtitle" dark></v-subheader>
      <v-list two-line>
        <template v-for="user in $store.state.users.list">
          <v-subheader v-if="user.header" :key="user.id" v-text="user.header"></v-subheader>
          <v-divider v-else-if="user.divider" :key="user.id" v-bind:inset="user.inset"></v-divider>
          <v-list-tile avatar v-else v-bind:key="user.id" href="javascript:;" download target="_blank">
            <v-list-tile-avatar>
              <img v-bind:src="user.avatar">
            </v-list-tile-avatar>
            </v-list-tile-avatar>
            <v-list-tile-content>
              <v-list-tile-title v-html="user.name"></v-list-tile-title>
              <v-list-tile-sub-title v-html="user.username"></v-list-tile-sub-title>
            </v-list-tile-content>
          </v-list-tile>
        </template>
      </v-list>
    </v-flex>
    <v-flex xs12 sm6 offset-sm3>
      <nuxt-child/>
    </v-flex>
  </v-layout>
</template>
<script>
export default {
  async fetch({ store, params, app }) {
    let users;
    try {
      users = await app.$axios.get('/users').then(res => res.data);
    } catch (error) {
      return console.error(error);
    }
    store.commit('users/setUsers', users);
  },
  data() {
    return { subtitle: 'Users', users: [] }
  }
}
</script>
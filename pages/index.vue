<template>

  <v-list subheader>
    <v-subheader>Recent chat</v-subheader>
    <v-list-tile
      v-for="item in items"
      :key="item.title"
      avatar
      @click="nextlink(item.id)"
    >
      <v-list-tile-avatar>
        <img src="https://cdn.vuetifyjs.com/images/lists/4.jpg">
      </v-list-tile-avatar>

      <v-list-tile-content>
        <v-list-tile-title v-html="item.title"></v-list-tile-title>
      </v-list-tile-content>

      <v-list-tile-action>
        <v-icon :color="item.active ? 'teal' : 'grey'">chat_bubble</v-icon>
      </v-list-tile-action>
    </v-list-tile>
  </v-list>



</template>

<script>
  export default {
    async asyncData({ app }) {
      const baseUrl = 'https://jsonplaceholder.typicode.com/todos'
      const response = await app.$axios.$get(baseUrl)
      console.log(response)
      return {
        items: response
      }
    },
    data () {
      return {
        items: []
        //   { active: true, title: 'Jason Oner', avatar: 'https://cdn.vuetifyjs.com/images/lists/1.jpg' },
        //   { active: true, title: 'Ranee Carlson', avatar: 'https://cdn.vuetifyjs.com/images/lists/2.jpg' },
        //   { title: 'Cindy Baker', avatar: 'https://cdn.vuetifyjs.com/images/lists/3.jpg' },
        //   { title: 'Ali Connors', avatar: 'https://cdn.vuetifyjs.com/images/lists/4.jpg' }
        // ]
      }
    },

    watch: {
      isUpdating (val) {
        if (val) {
          setTimeout(() => (this.isUpdating = false), 3000)
        }
      }
    },

    methods: {
      nextlink (user_id) {
        this.$router.push({name: 'user-user_id', params:{user_id:user_id } })
      },
      remove (item) {
        const index = this.friends.indexOf(item.name)
        if (index >= 0) this.friends.splice(index, 1)
      }
    }
  }
</script>

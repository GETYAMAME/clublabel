<template>
  <v-app light>
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
    >
    <span>🌈 ClubHouse用ラベルメーカー</span>
    </v-app-bar>
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
    <v-footer
      :absolute="!fixed"
      app
    >
      <span>&copy; {{ new Date().getFullYear() }}</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'アイウエオ',
          to: '/'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'アイウエオ',
          to: '/inspire'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js'
    }
  }
}
</script>

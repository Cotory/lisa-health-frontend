<template>
  <v-app>

    <v-toolbar
      app
      :clipped-left="clipped"
      color="primary"
      dark
    >
      <v-toolbar-title v-text="realTitle" ></v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn icon @click.stop="rightDrawer = !rightDrawer">
        <v-icon>menu</v-icon>
      </v-btn>
    </v-toolbar>
    <v-content>
      <router-view></router-view>
    </v-content>
    <v-navigation-drawer
      temporary
      :right="right"
      v-model="rightDrawer"
      fixed
      app
    >
      <v-list>
        <v-list-tile ripple to="/">
          <v-list-tile-action>
            <div class="iconfont">&#xe612;</div>
          </v-list-tile-action>
          <v-list-tile-title>首页</v-list-tile-title>
        </v-list-tile>
        <v-list-tile ripple to="/diagnosis">
         <v-list-tile-action>
           <div class="iconfont">&#xe617;</div>
         </v-list-tile-action>
         <v-list-tile-title>智能诊断</v-list-tile-title>
       </v-list-tile>
        <v-list-tile ripple to="/aids">
          <v-list-tile-action>
            <div class="iconfont">&#xe62d;</div>
          </v-list-tile-action>
          <v-list-tile-title>急救查询</v-list-tile-title>
        </v-list-tile>
        <v-list-tile ripple to="/symlab">
          <v-list-tile-action>
            <div class="iconfont">&#xe626;</div>
          </v-list-tile-action>
          <v-list-tile-title>疾病百科</v-list-tile-title>
        </v-list-tile>
        <v-list-tile ripple to="/hospitalsearch">
          <v-list-tile-action>
            <div class="iconfont">&#xe619;</div>
          </v-list-tile-action>
          <v-list-tile-title>医院查询</v-list-tile-title>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-footer :fixed="fixed" app>
      <span>&copy; 2018</span>
    </v-footer>
    <vue-progress-bar></vue-progress-bar>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld'

export default {
  name: 'App',
  components: {
    HelloWorld,
  },
  data () {
    return {
      clipped: false,
      drawer: true,
      fixed: false,
      items: [{
        icon: 'bubble_chart',
        title: 'Inspire'
      }],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Lisa Health'
    }
  },
  computed: {
    realTitle() {
      return this.$route.meta.title || this.title
    }
  },
  methods:{
    Gohome() {
      <router-link to="/diagnosis"></router-link>
    }
  },
  created () {
    //  this.$Progress.start()
    //  hook the progress bar to start before we move router-view
    this.$router.beforeEach((to, from, next) => {
      //  does the page we want to go to have a meta.progress object
      if (to.meta.progress !== undefined) {
        let meta = to.meta.progress
        // parse meta tags
        this.$Progress.parseMeta(meta)
      }
      //  start the progress bar
      this.$Progress.start()
      //  continue to next page
      next()
    })
    //  hook the progress bar to finish after we've finished moving router-view
    this.$router.afterEach((to, from) => {
      //  finish the progress bar
      this.$Progress.finish()
    })
  }
}
</script>

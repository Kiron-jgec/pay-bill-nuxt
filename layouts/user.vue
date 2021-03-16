<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
    <v-spacer />
    <v-btn
        icon
        @click.stop="miniVariant = !miniVariant"
        class="navExpandbtn right"
      >
        <v-icon>mdi-{{ `chevron-${miniVariant ? 'right' : 'left'}` }}</v-icon>
      </v-btn>



      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
     
     <!-- logout -->
          <v-list class="logout">
        <v-list-item
          
          to="/"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>mdi-chart-bubble</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title  />
            Log out
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
      elevation="0"
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      
    
     
      <v-toolbar-title v-text="title" />

    

  <v-spacer></v-spacer>
      <v-btn
  depressed
  elevation="1"
  to="/user/new-bill"
  color="#1365ff"
  class="text-capitalize white--text mr-4"
>   New Bill </v-btn>



     
      <v-btn
        icon
        @click.stop="rightDrawer = !rightDrawer"
      >
        <v-icon>mdi-menu</v-icon>
      </v-btn>
    </v-app-bar>
    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
    <v-navigation-drawer
      v-model="rightDrawer"
      :right="right"
      temporary
      fixed
    >
      <v-list>
        <v-list-item @click.native="right = !right">
          <v-list-item-action>
            <v-icon light>
              mdi-repeat
            </v-icon>
          </v-list-item-action>
          <v-list-item-title>Switch drawer (click me)</v-list-item-title>
        </v-list-item>
      </v-list>
      
    </v-navigation-drawer>
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
      clipped:true,
      drawer: false,
      fixed: false,
     
      items: [
        {
          icon: 'mdi-text-box-plus-outline',
          title: 'New Bill',
          to: '/user/new-bill'
        },
           {
          icon: 'mdi-view-dashboard-outline ',
          title: 'Dashboard',
          to: '/user/dashboard'
        },
        {
          icon: 'mdi-account-circle-outline',
          title: 'Profile',
          to: '/user/profile'
        },
          {
          icon: 'mdi-cog-outline',
          title: 'Settings',
          to: '/user/settings'
        },
         {
          icon: 'mdi-help-circle-outline',
          title: 'Help',
          to: '/user/help'
        }
      ],
        items2: [
       
        
      
         {
          title: 'Log In',
          to: '/login'
        },
         {
          title: 'Sign Up',
          to: '/sign-up'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Shop/company Name'
    }
  }
}
</script>

<style scoped>
.logout
{
  position: fixed;
  bottom: 0 !important;
}
.navExpandbtn
{
 
}
</style>

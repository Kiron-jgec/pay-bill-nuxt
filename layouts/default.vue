<template>
  <v-app dark>
    <!-- <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
    >
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
    </v-navigation-drawer> -->
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
      flat
      class="primary px-6"
      dark
    >
   
   
     
     
      <v-toolbar-title v-text="title" />
      <v-spacer />
            <v-tabs right class="" style="width:fit-content">
    <v-tab   v-for="(item, i) in items"  :key="i" v-text="item.title" :to="item.to"></v-tab>
  
  </v-tabs>
<!-- <v-list class="transparent"  dense>
      <v-list-item-group v-model="model" class="d-flex py-0 my-0 ">
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          
          <v-list-item-content class="text-center">
            <v-list-item-title v-text="item.title" class="linkList "></v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list-item-group>
    </v-list> -->
  

    
    
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
      fixed: true,
       model:1,
      items: [
        {
          title: 'Home',
          to: '/'
        },
        {
          title: 'About',
          to: '/about-us'
        },
         {
          title: 'Contact',
          to: '/contact-us'
        },
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
      title: 'Pay Bill'
    }
  }
}
</script>


<style scoped lang="scss">
*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
 
}

.linkList
{
font-size: 16px !important;
}
</style>
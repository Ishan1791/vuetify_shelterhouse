
<template>
  <v-app id="inspire">
    <v-navigation-drawer 
      v-model="drawer"
      app
    >
      <v-list
        dense
        nav
      >
        <v-list-item
          v-for="item in items"
          :key="item.title"
          :to="item.to"
          link
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <!-- Top Nav bar -->
    <v-app-bar 
      class="red white--text"
      app>
      <v-app-bar-nav-icon class="white--text" @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>Shelter House</v-toolbar-title>
    </v-app-bar>

    <!-- Bottom Nav bar -->
    <v-bottom-navigation 
      app
      fixed
      grow
      background-color="red"
      
      >
      <v-btn  value="home" to="/">
        

        <v-icon class = "white--text">mdi-home</v-icon>
      </v-btn>

      <v-btn value="finder" to="/finder">
        
        <v-icon class = "white--text">mdi-magnify</v-icon>
      </v-btn>

      <v-btn value="flashcard" to="/flashcard">
       

        <v-icon class = "white--text">mdi-cards</v-icon>
      </v-btn>

      <v-btn value="videos" to="/videos">
        

        <v-icon class = "white--text">mdi-filmstrip-box-multiple</v-icon>
      </v-btn>
  </v-bottom-navigation>

    <v-main>
      <!--  -->
      <!-- If using vue-router -->
      <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
  export default {
    data: () => ({ 
      drawer: null,
      items: [
        { title: 'Administration', icon: 'mdi-cog', to: '/admin' },
       
      ],
    }),
  }
</script>

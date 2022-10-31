<template>
  <v-container class="grey">
    <v-row>
      <v-col col="12">
        <v-img
          :src="landingImage"
          height="361"
          class="grey darken-4"
            >
        </v-img>
      </v-col>
      <v-col col="12" align="center">
        <h4 class="red--text">For Emergency <a href="tel:211" id="call-button">Dial 2-1-1</a></h4>  
      </v-col>
    </v-row>
    <v-row>
      
      <v-col col="12" align="center">
        <v-card
            color="blue-grey darken-3"
            
          >
            

            <v-card-subtitle class="white--text">We envision a community in which every individual has a stable home and feels loved and respected in the society they live in.</v-card-subtitle>

            
          </v-card>    
      </v-col>
    </v-row>

  </v-container>

</template>


<script>
export default {
  data: () => ({
    landingImage: require('../assets/shelter.jpg'),
  }),
}
</script>
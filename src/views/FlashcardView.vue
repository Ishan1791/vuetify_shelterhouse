<template>
  <div class="about text-center">
    <v-carousel cycle hide-delimiters :show-arrows="false">
        <v-carousel-item
            v-for="(card,i) in cards"
            :key="i"
        >

        <v-sheet
          max-width="300"
          class="mx-auto mt-8 rounded-circle red white--text text-h4"
          elevation="6"
          height="300"
          width="100%"
        >
        <v-container fill-height fluid>
        <v-row align="center"
            justify="center">
            <v-col>{{card.stat}}%<br>{{card.detail}}</v-col>
        </v-row>
        </v-container></v-sheet>
        <v-sheet
          max-width="128"
          class="mx-auto mt- rounded-circle red darken-4 white--text text-h4 float-right"
          elevation="6"
          height="128"
          width="100%"
        >
        </v-sheet>
        </v-carousel-item>
    </v-carousel>
  </div>
</template>
<script>
  export default {
    data: () => ({
      cards: [],
    }),
  async created() {
      const response = await fetch("https://1he3pmvbyd.execute-api.us-east-1.amazonaws.com/stat")
      this.cards = await response.json();
  }
  }
</script>
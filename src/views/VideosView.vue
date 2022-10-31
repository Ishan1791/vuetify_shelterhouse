<template>
    <v-container fluid>
    <v-row dense>
        <v-col
        v-for="card in cards"
        :key="card.title"
        :cols="card.flex"
        >
        <a :href="card.video_url" target="_blank">
        <v-card>
            <v-img
            :src="card.src"
            class="white--text align-end"
            gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
            height="200px"
            >
            <v-card-subtitle v-text="card.title"></v-card-subtitle>  
            </v-img>
            
            
        </v-card>
        </a>
        </v-col>
    </v-row>
    </v-container>
</template>
<script>
  export default {
    data: () => ({
      cards: [
        { title: 'Misconception about Homelessness', video_url:'https://youtu.be/Q3yQJG0qnd0', src: require('../assets/mic/mic1.jpg'), flex: 12 },
        { title: 'Different Categories of Homelessness', video_url:'https://youtu.be/RklWwgwH3dw', src: require('../assets/mic/mic8.jpg'), flex: 6 },
        { title: 'Impact of Covid on Assisting Organizations', video_url:'https://youtu.be/_0VyK_dEtRk', src: require('../assets/mic/mic5.jpg'), flex: 6 },
        { title: 'Fighting Homelessness during Covid', video_url:'https://youtu.be/TubNSLGeo6M', src: require('../assets/mic/mic6.jpg'), flex: 12 },
        { title: 'Impact of Covid on the Homeless', video_url:'https://youtu.be/PXIn9osgYVc',src: require('../assets/mic/mic4.jpg'), flex: 6 },
        { title: 'Kristen Corley - Covenant House', video_url:'https://youtu.be/pi6RJ70Q7Ak', src: require('../assets/mic/mic7.jpg'), flex: 6 },
        { title: 'Interview with Connie Mercer CEO of Homefront', video_url:'https://youtu.be/vSms4tiUxws', src: require('../assets/mic/mic11.jpg'), flex: 12 },
        { title: 'Unique Challenges of Homelessness in NJ', video_url:'https://youtu.be/L58AtwqnFj4', src: require('../assets/mic/mic9.jpg'), flex: 6 },
        { title: 'Dan McGuire - Homeless Solutions', video_url:'https://youtu.be/0_Xnm43q13c', src: require('../assets/mic/mic13.jpg'), flex: 6 },

      ],
    }),
  }
</script>
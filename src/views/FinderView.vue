<template>
    <div class="finder">
        <v-form>
            <v-container>
                <v-row dense >
                    <v-col cols="3">
                        <v-text-field
                            dense
                            clearable
                            label="County"
                            id="fCounty"
                            v-model="fCounty"
                        ></v-text-field>
                    </v-col>
                    <v-col cols="4">
                        <v-text-field
                            dense
                            clearable
                            label="City / Town"
                            id="fCity"
                            v-model="fCity"
                        ></v-text-field>
                    </v-col>
                    <v-col cols="4">
                        <v-text-field
                            dense
                            clearable
                            label="Name"
                            id="fName"
                            v-model="fName"
                        ></v-text-field>
                    </v-col>
                    <v-col cols="1">
                        <v-btn
                            icon
                            color="red"
                            @click="filterShelter"
                            >
                            <v-icon>mdi-magnify</v-icon>
                        </v-btn>


                       
                    </v-col>
                </v-row>
            </v-container>
        </v-form>
        
        <v-container class="grey lighten-5">
        <v-row v-for="shelter in shelters" :key="shelter.id">
        <v-col >
            <v-card>
                <v-card-title>{{shelter.name}}</v-card-title>
                <v-divider class="red mx-2"></v-divider>
                <v-card-text>
                    <v-row no-gutters>
                        <v-col align="left">Emergency:</v-col>
                        <v-col align="center">{{shelter.emergencyUnits}} units</v-col>
                        <v-col align="left">Transitional:</v-col>
                        <v-col align="center">{{shelter.transitionalUnits}} units</v-col>
                        
                    </v-row>
                    <v-row no-gutters>
                        <v-col align="left">Youth:</v-col>
                        <v-col align="center">
                            <p v-if="shelter.acceptsYouth"><v-icon class = "red--text">mdi-check</v-icon></p>
                            <p v-else><v-icon class = "red--text">mdi-close</v-icon></p>
                             
                        </v-col>
                        <v-col align="left">Family:</v-col>
                        <v-col align="center">
                            <p v-if="shelter.acceptsFamily"><v-icon class = "red--text">mdi-check</v-icon></p>
                            <p v-else><v-icon class = "red--text">mdi-close</v-icon></p>
                        </v-col>
                        
                    </v-row>
                    <v-row no-gutters>
                        <v-col align="left">Individual</v-col>
                        <v-col align="center">
                            <p v-if="shelter.acceptsIndividual"><v-icon class = "red--text">mdi-check</v-icon></p>
                            <p v-else><v-icon class = "red--text">mdi-close</v-icon></p>
                       
                        </v-col>
                        <v-col align="left">Gender Restrictions:</v-col>
                        <v-col align="center">
                            <p v-if="shelter.hasGenderRestrictions"><v-icon class = "red--text">mdi-check</v-icon></p>
                            <p v-else><v-icon class = "red--text">mdi-close</v-icon></p>
                            
                        </v-col>
                        
                    </v-row>
                </v-card-text>
                <v-divider class="red mx-2"></v-divider>
                <v-card-text>
                    {{getFullStreetAddress(shelter)}}
                </v-card-text>
                <v-divider class="red mx-2"></v-divider>
                <v-card-text>{{shelter.phoneNumber}}</v-card-text>
                <v-divider class="red mx-2"></v-divider>
                <v-row>
                    <v-col>
                        <v-btn plain @click="openMap(shelter)">
                            <v-icon class = "red--text">mdi-map-marker</v-icon>Directions
                        </v-btn>
                    </v-col>
                    <v-col align="center">
                        <v-btn plain @click="callNumber(shelter.phoneNumber)">
                            <v-icon class = "red--text">mdi-phone</v-icon>Call
                        </v-btn>
                    </v-col>
                </v-row>   
                
            </v-card>
        </v-col>
        
        </v-row>
        </v-container>
    </div>
      
    
</template>
<script>
    export default {
    data: () => ({
        shelters: [],
        fCounty: '',
        fCity: '',
        fName: '',
    }),
    async created() {
        const response = await fetch("https://1he3pmvbyd.execute-api.us-east-1.amazonaws.com/shelter")
        this.shelters = await response.json();
    },
    methods:{
        async filterShelter(){
        //console.warn('In Filter Shelter')
        let filterParameters = {
            addressCounty: this.fCounty,
            addressCity: this.fCity,
            name: this.fName
        } 
        //console.warn(JSON.stringify(filterParameters))
        const response = await fetch("https://1he3pmvbyd.execute-api.us-east-1.amazonaws.com/search",{
        method: "post",
        headers: {
            "Content-Type":"application/json"
        },
        body: JSON.stringify(filterParameters)
        })
        //let res = await response.text()
        let res = await response.json()
        //console.warn('Printing res')
        //console.warn(JSON.stringify(res))
        this.shelters = res

        },
        getFullStreetAddress(shelter){
            return shelter.addressNumber + ' ' + shelter.addressStreet + ', ' + shelter.addressCity + ', ' + shelter.addressState + ' ' + shelter.addressZip;
        },
        getFullCityStateZip(shelter){
            return shelter.addressCity + ', ' + shelter.addressState + ' ' + shelter.addressZip;
        },
        openMap(shelter){
            let mapAddress = shelter.addressNumber+'+'+shelter.addressStreet+'+'+shelter.addressZip
            let val = mapAddress.replaceAll(" ", "+");
            if ( /* if we're on iOS, open in Apple Maps */
                navigator.platform.indexOf("iPhone") != -1 ||
                navigator.platform.indexOf("iPod") != -1 ||
                navigator.platform.indexOf("iPad") != -1) {
                //val = 'maps://maps.google.com/maps/dir/?api=1&' + val + '&dir_action=navigate';
                val = 'https://www.google.com/maps/dir/?api=1&destination=' + val + '&dir_action=navigate';
                window.open(val);
            }
            else {
                /* else use Google */
                val = 'https://www.google.com/maps/dir/?api=1&destination=' + val + '&dir_action=navigate';
                window.open(val);
            }
        },
        callNumber(phoneNumber){
            phoneNumber = 'tel:' +phoneNumber;
            window.open(phoneNumber);
        },
    }
  }
</script>
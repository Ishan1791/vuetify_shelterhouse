<template>
  <v-form v-model="valid">
    <v-container>
      <v-row>
        <v-col cols="12">
          <v-text-field
            v-model="name"
            :rules="nameRules"
            label="Name"
            required
          ></v-text-field>
        </v-col>

        <v-col cols="4">
          <v-text-field
            v-model="emergencyUnits"
            label="# of Emergency Units"
          ></v-text-field>
        </v-col>

        <v-col cols="4">
          <v-text-field
            v-model="transitionalUnits"
            label="# of Transitional Units"
          ></v-text-field>
        </v-col>
        <v-col cols="4">
          <v-text-field
            v-model="phoneNumber"
            :rules="nameRules"
            label="Phone Number"
            required
          ></v-text-field>
        </v-col>
        <v-col cols="3">
          <v-checkbox
            v-model="acceptsYouth"
            label="Accepts Youth?"
          ></v-checkbox>
        </v-col>

        <v-col cols="3">
          <v-checkbox
            v-model="acceptsFamily"
            label="Accepts Family?"
          ></v-checkbox>
        </v-col>
        <v-col cols="3">
          <v-checkbox
            v-model="acceptsIndividual"
            label="Accepts Individuals?"
          ></v-checkbox>
        </v-col>
        <v-col cols="3">
          <v-checkbox
            v-model="hasGenderRestrictions"
            label="Gender Restrictions?"
          ></v-checkbox>
        </v-col>

        <v-col cols="1">
          <v-text-field
            v-model="addressNumber"
            label="Number"
            
          ></v-text-field>
        </v-col>
        <v-col cols="4">
          <v-text-field
            v-model="addressStreet"
            :rules="nameRules"
            label="Street"
            required
          ></v-text-field>
        </v-col>
        <v-col cols="2">
          <v-text-field
            v-model="addressCity"
            :rules="nameRules"
            label="City"
            required
          ></v-text-field>
        </v-col>
        <v-col cols="2">
          <v-text-field
            v-model="addressCounty"
            :rules="nameRules"
            label="County"
            required
          ></v-text-field>
        </v-col>
        <v-col cols="2">
          <v-text-field
            v-model="addressState"
            :rules="nameRules"
            label="State"
            required
          ></v-text-field>
        </v-col>
        <v-col cols="1">
          <v-text-field
            v-model="addressZip"
            :rules="nameRules"
            label="Zip"
            required
          ></v-text-field>
        </v-col>
        <v-col cols="1">
          <v-btn block color="red white--text" @click="addShelter">
            Add
          </v-btn>  
        </v-col>
      </v-row>
      
    </v-container>
    <v-divider class="red mx-2"></v-divider>
    <v-divider class="red mx-2"></v-divider>
    <v-container>
      <div pa-md-4>
        <h4>
        <v-row pa-md-4> 
        <v-col cols="4">Shelter Name</v-col>
        <v-col cols="7">Shelter Address  </v-col>
        <v-col cols="1"> </v-btn></v-col>
      </v-row>
      </h4>
      </div>
      <v-divider class="grey"></v-divider>
      <v-divider class="grey"></v-divider>
      <div pa-md-4 class="shelters" v-for="shelter in shelters" :key="shelter.id">
      
      <v-row pa-md-4> 
        <v-col cols="4">{{shelter.name}}</v-col>
        <v-col cols="7">{{shelter.addressNumber}} {{shelter.addressStreet}}, {{shelter.addressCity}}, {{shelter.addressCounty}}, {{shelter.addressState}} {{shelter.addressZip}}  </v-col>
        <v-col cols="1"><v-btn block color="red white--text" @click="removeShelter">Delete</v-btn></v-col>
      </v-row>
      <v-divider class="grey"></v-divider>      
    </div>
    </v-container>
    

  
  </v-form>
  
</template>
<script>
  export default {
    data: () => ({
      id:'',
      name: '',
      emergencyUnits: null, 
      transitionalUnits: null,
      acceptsYouth: false,
      acceptsFamily: false,
      acceptsIndividual: false,
      hasGenderRestrictions: false,
      addressNumber: '',
      addressStreet: '',
      addressCity: '',
      addressCounty: '',
      addressState: '',
      addressZip: '',
      phoneNumber: '',
      shelters: [],

      
      
    }),
  
  async created() {
  const response = await fetch("https://1he3pmvbyd.execute-api.us-east-1.amazonaws.com/shelter")
  this.shelters = await response.json();
  
  },

  methods: {
    async addShelter() {
      if (this.name === '' ){
          alert('Shelter Data Entry Form is incomplete. Please fill out every field.')
          return
      }
      let shelterId = Math.floor(Math.random() * (999999999 - 100000000) + 999999999 )
      let shelter = {
          id: shelterId.toString(),
          name: this.name,
          emergencyUnits: this.emergencyUnits, 
          transitionalUnits: this.transitionalUnits,
          acceptsYouth: this.acceptsYouth,
          acceptsFamily: this.acceptsFamily,
          acceptsIndividual: this.acceptsIndividual,
          hasGenderRestrictions: this.hasGenderRestrictions,
          addressNumber: this.addressNumber,
          addressStreet: this.addressStreet,
          addressCity: this.addressCity,
          addressCounty: this.addressCounty,
          addressState: this.addressState,
          addressZip: this.addressZip,
          phoneNumber: this.phoneNumber,
          dummyId: 'dummy'
      } 
      await fetch("https://1he3pmvbyd.execute-api.us-east-1.amazonaws.com/shelter",{
        method: "post",
        headers: {
          "Content-Type":"application/json"
        },
        body: JSON.stringify(shelter)
      })

      this.shelters.push(shelter)

      this.id=''
      this.name=''
      this.emergencyUnits=null
      this.transitionalUnits=null
      this.acceptsYouth=false
      this.acceptsFamily=false
      this.acceptsIndividual=false
      this.hasGenderRestrictions=false
      this.addressNumber=''
      this.addressStreet=''
      this.addressCity=''
      this.addressCounty=''
      this.addressState=''
      this.addressZip=''
      this.phoneNumber=''

    } ,
      
    async removeShelter (shelterId){
      await fetch("https://1he3pmvbyd.execute-api.us-east-1.amazonaws.com/shelter",{
        method: "delete",
        headers: {
          "Content-Type":"application/json"
        },
        body: JSON.stringify({id: shelterId})
      })
      this.shelters = this.shelters.filter(s=>s.id!==shelterId)
    }
    
  }



  }
</script>
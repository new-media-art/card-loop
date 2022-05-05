<template>
<div class="x"> 
<v-img
          
          src="https://cdn.pixabay.com/photo/2020/07/12/07/47/bee-5396362_1280.jpg"
        >
   

  <v-card
    max-width="1200"
    class="mx-auto"
  >
   
<v-img
          
          src="https://cdn.pixabay.com/photo/2020/07/12/07/47/bee-5396362_1280.jpg"
        >

    <v-container>
      <v-row dense>
        <v-col cols="12">



         <v-card
       class="mx-auto my-12  pa-6"
      max-width="374"
        
       
      >
            
            <v-radio-group
              v-model="ex7"
              column
              
              
            >
              <v-radio
                label="very hot"
                color="red"
                value="red"
              ></v-radio>
              <v-radio
                label="hot"
                color="red darken-3"
                value="red darken-3"
              ></v-radio>
                <v-radio
                label="warm"
                color="orange darken-3"
                value="orange darken-3"
              ></v-radio>
               
               <v-radio
                label="chilly"
                color="orange"
                value="orange"
              ></v-radio>
             
              <v-radio
                label="cold"
                color="indigo"
                value="indigo"
              ></v-radio>
              <v-radio
                label="very cold"
                color="indigo darken-3"
                value="indigo darken-3"
              ></v-radio>
             
            </v-radio-group>


              <v-menu
                  v-model="menu1"
                  :close-on-content-click="false"
                  max-width="290"
                >
                <template v-slot:activator="{ on, attrs }">
                  <div-field
                    :value="computedDateFormattedMomentjs"
                    clearable
                    label="Formatted with Moment.js"
                    readonly
                    v-bind="attrs"
                    v-on="on"
                    @click:clear="date = null"
                  ></div-field>
              </template>
          <v-date-picker
            v-model="date"
            @change="menu1 = false"
          ></v-date-picker>
        </v-menu>  

          <div class="text-center">
              <v-btn
                rounded
                color="primary"
                dark
              >
                Search flights
              </v-btn>
            </div>
            
            </v-card>
       
      
       
       
        </v-col>

        <v-col
          
          cols="12"
        >
        
         


        </v-col>
      
       <v-col
          
          cols="12"
        >



     <v-data-table
              :headers="headers"
              :items="destinationsList"
              class="elevation-2 pa-12"
            >
              <template v-slot:[`item.temperature`]="{ item }">
                <v-chip
                  :color="getColor(item.temperature)"
                  dark
                >
              {{ item.temperature }}
      </v-chip>
      
    </template>
   
  </v-data-table>

        

        </v-col>
      
      </v-row>
       <button v-on:click="doThis">ddd</button>
    </v-container>
     </v-img>
  </v-card>
</v-img>

  </div>

</template>
      


<script>
   import moment from 'moment'
  import { format, parseISO } from 'date-fns'
  export default {
    data () {
      return {
        ex7: 'red',
        date: format(parseISO(new Date().toISOString()), 'yyyy-MM-dd'),
        menu1: false,
        menu2: false,
        
        headers: [
          {
            text: 'Destinations',
            align: 'start',
            sortable: false,
            value: 'name',
          },
          { text: 'Temperature C°', value: 'temperature' },
          { text: 'Weather icon', value: 'icon' },
          { text: 'See details', value: 'see details' },
           
          
        ],
        destinationsList: [
          {
            name: 'Lisboa',
            temperature: 40,
            icon: '01d.png',
            details: 'see details'
            
          },
          {
            name: 'Amsterdam',
            temperature: 39,
            icon:'01d.png',
            
          },
          {
            name: 'London',
            temperature: 37,
            icon: '01d.png',
            
          },
          {
            name: 'Milan',
            temperature: 36,
            icon: '01d.png',
            
          },
          {
            name: 'Zagreb',
            temperature: 35,
            icon: '01d.png',
            
          },
          {
            name: 'Stockholm',
            temperature: 33,
            icon: '01d.png',
            
          },
          {
            name: 'Warsaw',
            temperature: 25,
            icon: '01d.png',
            
          },
          {
            name: 'London',
            temperature: 22,
            icon: '01d.png',
            
          },
          {
            name: 'Budapest',
            temperature: 19,
            icon: '01d.png',
            
          },
          {
            name: 'Helsinki',
            temperature: 15,
            icon: '01d.png',
            
          },
        ],
      }
    }
    ,
    methods: {
      getColor (temperature) {
        if (temperature > 35) return 'dark orange'
        else if (temperature > 20) return 'yellow'
        else return 'blue'
      }
    },
       computed: {
      computedDateFormattedMomentjs () {
        return this.date ? moment(this.date).format('dddd, MMMM Do YYYY') : ''
      },
      computedDateFormattedDatefns () {
        return this.date ? format(parseISO(this.date), 'EEEE, MMMM do yyyy') : ''
      },
    },
  }
  

</script>

<style>
  .x {
    background-color: black;
  }
</style>
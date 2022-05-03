<template>
  
<div>


  

          



<v-card
       
        
       
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
            
            </v-card>

            <!--Date picker-->
            <v-card
               
            >

            

            <v-menu
                  v-model="menu1"
                  :close-on-content-click="false"
                  max-width="290"
                >
                <template v-slot:activator="{ on, attrs }">
                  <v-text-field
                    :value="computedDateFormattedMomentjs"
                    clearable
                    label="Formatted with Moment.js"
                    readonly
                    v-bind="attrs"
                    v-on="on"
                    @click:clear="date = null"
                  ></v-text-field>
              </template>
          <v-date-picker
            v-model="date"
            @change="menu1 = false"
          ></v-date-picker>
        </v-menu>  

            
          </v-card>






       
 <v-card
              
                    >

           <v-data-table
              :headers="headers"
              :items="destinationsList"
              class="elevation-1"
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
 
        </v-card>

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
          { text: 'Temperature', value: 'temperature' },
          { text: 'Weather icon', value: 'icon' },
          
        ],
        destinationsList: [
          {
            name: 'Lisboa',
            temperature: 40,
            icon: '01d.png',
            
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
            temperature: 21,
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
        if (temperature > 35) return 'red'
        else if (temperature > 20) return 'orange'
        else return 'green'
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
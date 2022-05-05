<template>
  <v-card
    max-width="400"
    class="mx-auto"
  >
   

   

    <v-container>
      <v-row dense>
        <v-col cols="12">



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
       
       
       
       
        </v-col>

        <v-col
          
          cols="12"
        >
          
          
            <v-card
               
            >

            

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

            
          </v-card>
          
         
         
        </v-col>
      
       <v-col
          
          cols="12"
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

        

        </v-col>
      
      </v-row>
    </v-container>
  </v-card>
</template>
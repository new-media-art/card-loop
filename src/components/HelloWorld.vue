<template>
  <v-data-table
    :headers="headers"
    :items="flightDestinations"
    sort-by="temperature"
    class="elevation-1"
  >
    <template v-slot:top>




      <v-toolbar
        flat
      >
        <v-toolbar-title>Destinations</v-toolbar-title>
        <v-divider
          class="mx-4"
          inset
          vertical
        ></v-divider>
        <v-spacer></v-spacer>


        <v-dialog
          v-model="dialog"
          max-width="500px"
        >

        <!--
          <template v-slot:activator="{ on, attrs }">

              
            <v-btn
              color="primary"
              dark
              class="mb-2"
              v-bind="attrs"
              v-on="on"
            >
              New Item
            </v-btn>
            
          </template>
            -->

          <v-card>
            <v-card-title>
              <span class="text-h5">Selected destination</span>
            </v-card-title>

            <v-card-text>
              <v-container>
                <v-row>

                  <v-col
                    cols="6"
                  >
                    <div>Destination: {{ selectedItem.name }}</div>
                    
                  </v-col>
                
                  
                  <v-col
                    cols="6"
                    
                  >
                    <div>Temperature: {{ selectedItem.temperature }}  C°</div>
                  </v-col>
                
                 <v-col
                    cols="6"
                    
                  >
                    <div>Price: {{ selectedItem.price }}  €</div>
                  </v-col>

                     <v-col
                    cols="4"
                    
                  >
                 
                    <v-icon
                        large
                        color="green darken-2"
                        >
                        mdi-weather-lightning
                        </v-icon>
                  </v-col>
                 </v-row>
                  
                
                 
                
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn
                color="blue darken-1"
                text
                @click="close"
              >
                Cancel
              </v-btn>
              <v-btn
                color="blue darken-1"
                text
                @click="select"
              >
                Select
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>
      
      </v-toolbar>




    </template>
    <template v-slot:[`item.actions`]="{ item }">

        <v-btn
        @click="selectItem(item)"
        color="white"
        small
        > Select 

            <v-icon
                small
                class="mr-2"
                color="blue"
                >
                mdi-arrow-right-thick
            </v-icon>
        </v-btn>

      


    
    
    </template>
    <template v-slot:no-data>
      <v-btn
        color="primary"
        @click="initialize"
      >
        Reset
      </v-btn>
    </template>
  </v-data-table>
</template>

<script>
  export default {
    data: () => ({
      dialog: false,
      dialogDelete: false,
      headers: [
        {
            text: 'Destinations',
            align: 'start',
            sortable: false,
            value: 'name',
        },
         { text: 'Temperature C°', value: 'temperature' },
          { text: 'Weather icon', value: 'icon' },
           {text: 'price €', value: 'price' },
         { text: 'Actions', value: 'actions', sortable: false },
      ],
      flightDestinations: [],
      editedIndex: -1,
      selectedItem: {
        name: '',
        temperature: 0,
        price: 0,
        
      },
      defaultItem: {
        name: '',
        temperature: 0,
        price: 0,
        
      },
    }),

   

    watch: {
      dialog (val) {
        val || this.close()
      },
      dialogDelete (val) {
        val || this.closeDelete()
      },
    },

    created () {
      this.initialize()
    },

    methods: {
      initialize () {
        this.flightDestinations = [
          {
            name: 'Lisboa',
            temperature: 40,
            icon: '01d.png',
            price: 65.99,
            
            
          },
          {
            name: 'Amsterdam',
            temperature: 39,
            icon:'01d.png',
            price: 48.99,
            
          },
          {
            name: 'London',
            temperature: 37,
            icon: '01d.png',
            price: 33.99,
            
          },
          {
            name: 'Milan',
            temperature: 36,
            icon: '01d.png',
            price: 52.99,
            
          },
          {
            name: 'Zagreb',
            temperature: 35,
            icon: '01d.png',
            price: 44.99,
            
          },
          {
            name: 'Stockholm',
            temperature: 33,
            icon: '01d.png',
            price: 36.99,
            
          },
          {
            name: 'Warsaw',
            temperature: 25,
            icon: '01d.png',
            price: 120.99,
            
          },
          {
            name: 'London',
            temperature: 22,
            icon: '01d.png',
            price: 60.99,
            
          },
          {
            name: 'Budapest',
            temperature: 19,
            icon: '01d.png',
            price: 33.99,
            
          },
          {
            name: 'Helsinki',
            temperature: 15,
            icon: '01d.png',
            price: 49.88,
            
          },
        ]
      },

      selectItem (item) {
        this.editedIndex = this.flightDestinations.indexOf(item)
        this.selectedItem = Object.assign({}, item)
        this.dialog = true
      },

      

      

      close () {
        this.dialog = false
        this.$nextTick(() => {
          this.selectedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },

      closeDelete () {
        this.dialogDelete = false
        this.$nextTick(() => {
          this.selectedItem = Object.assign({}, this.defaultItem)
          this.editedIndex = -1
        })
      },

      select () {
        if (this.editedIndex > -1) {
          Object.assign(this.flightDestinations[this.editedIndex], this.selectedItem)
        } else {
          this.flightDestinations.push(this.selectedItem)
        }
        this.close()
      },
    },
  }
</script>
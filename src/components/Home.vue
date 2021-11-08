<template>
  <v-row justify="center">
    <v-dialog v-model="dialog" persistent max-width="project"> <!-- 경고창 -->
      <template v-slot:activator="{ on }"> <!-- on 은 액션창 생성 명령어 --> 
        <v-btn outlined color="white" dark v-on="on" > Login </v-btn>
      </template>
    
 
    




    <v-content>
      <v-container class="fill-height" fluid>
        <v-row align="center" justify="center">
          <v-col cols="12" sm="8" md="7">
            <v-card class="elevation-12">
               <v-window v-model="step">
               <v-window-item :value="1">
                  <v-row>
                    <v-col cols="12" md="8">
                     <v-card-text class="mt-50">
                       
                       <h1 class="text-center display-2 teal--text text--lighten-3">Sign in to MapDuck</h1>
                       <div class="text-center mt-3" mt-4>
                         <v-btn class="mx-2" fab-color ="black" outlined>
                           <v-icon>fab fa-neos</v-icon>
                         </v-btn>

                         <v-btn class="mx-2" fab-color="black" outlined>
                           <v-icon>fab fa-google-plus-g</v-icon>
                         </v-btn>

                         <v-btn class="mx-2" fab-color="black" outlined>
                           <v-icon>fab fa-facebook-f</v-icon>
                         </v-btn>

                       </div>
                       <h4 class="text-center mlt-4">Ensure your email for registration</h4>
                       <v-form>
                         <v-text-field
                         label="Email"
                         name="Email"
                         prepend-icon="email"
                         type="text"
                         color="teal accent-3"
                         :rules="inputRules"
                         > </v-text-field>
                         <v-text-field
                         id="password"
                         label="Password"
                         name="Password"
                         prepend-icon="lock"
                         type="password"
                         color="teal accent-3"
                         :rules="inputRules" ></v-text-field>

                       </v-form>
                       <h3 class="text-center mt-2">Forget your password ? </h3>
                     </v-card-text>
                     <div class="text-center mt-3">
                       <v-btn rounded color="teal lighten-3" dark>SIGN IN</v-btn> 
                       <v-btn rounded color="blue darken-1" text @click="dialog = false">Close</v-btn>
                     </div>
                     <h3 class="text-center mt-5"> </h3>
                    </v-col>
                    <v-col cols="12" md="4" class="teal lighten-3">
                      <v-card-text class="white--text mt-12">
                        <h1 class="text-center display-1">Hello, Friends !</h1>
                        <h5 class="text-center">Enter your personnel details and start journay with us</h5>
                      </v-card-text>

                      <div class="text-center">
                        <v-btn rounded outlined="" dark @click="step++">SIGN UP</v-btn>
                      </div> 
                      
                    </v-col>
                  </v-row>
               </v-window-item>
               <v-window-item :value="2">
                 <v-row class="">
                   <v-col cols="12" md="4" class="teal lighten-3">
                     <v-card-text class="white--text mt-12">
                       <h1 class="text-center display-1">Welcome Back! </h1>
                       <h5 class="text-center">To keep connected with us please login with your personnel info</h5>
                     </v-card-text>

                     <div class="text-center">
                       <v-btn rounded outlined dark @click="step--">SIGN IN</v-btn>
                     </div>

                     <div class="text-center"><v-card-text class="mt-2">
                       <v-btn rounded outlined dark @click="dialog = false">Close</v-btn>
                       </v-card-text>
                     </div>

                     
                   </v-col>

                   <v-col cols="12" md="8">
                     <v-card-text class="mt-12">
                       <h1 class="text-center display-2 teal--text text--lighten-3">Create Account</h1>
                      <div class="text-center mt-4">
                        <v-btn class="mx-2" fab-color="black" outlined>
                          <v-icon>fab fa-neos</v-icon>
                        </v-btn>
                        <v-btn class="mx-2" fab-color="black" outlined>
                         <v-icon>fab fa-google-plus-g</v-icon>
                       </v-btn>
                       <v-btn class="mx-2" fab-color="black" outlined>
                         <v-icon>fab fa-facebook-f</v-icon>
                       </v-btn>
                      </div>
                      <h4 class="text-center mt-4">Ensure your email for registration</h4>
                      <v-form>
                        <v-text-field
                        label="Name"
                        name="Name"
                        prepend-icon="person"
                        type="text"
                        color="teal lighten-3"/>

                        <v-text-field
                        label="Email"
                        name="Email"
                        prepend-icon="email"
                        type="text"
                        color="teal lighten-3" />

                        <v-text-field
                        label="Password"
                        name="Password"
                        prepend-icon="lock"
                        type="password"
                        color="teal lighten-3" />
                      </v-form>
                     <div class="text-center mt-3">
                      <v-btn rounded color="teal lighten-3" dark>SIGN UP</v-btn>
                     </div>
                     </v-card-text>
                   </v-col>
                 </v-row>
               </v-window-item>

               </v-window>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-content>
  
  </v-dialog>
  </v-row>
</template>


<script>
export default {
  name:'home',
  components:{

  },
  
  data: vm => ({
      step : 1,
      dialog: false,
      title:'',
      content:'',
      due:null,
      date: new Date().toISOString().substr(0, 10),
      dateFormatted: vm.formatDate(new Date().toISOString().substr(0, 10)),
      menu1: false,
      inputRules: [
          v => v.length >= 7 || 'Minimum lenght is 7 charachters' 
      ]
      
    }),

methods: {
         formatDate (date) {
        if (!date) return null
        const [year, month, day] = date.split('-')
        return `${year}/${month}/${day}`
      },
      parseDate (date) {
        if (!date) return null
        const [year, month, day] = date.split('/')
        return `${year}-${month.padStart(2, '0')}-${day.padStart(2, '0')}`
      },
    },
    computed: {
      computedDateFormatted () {
        return this.formatDate(this.date)
      },
    },
    watch: {
      date () {
        this.dateFormatted = this.formatDate(this.date)
      },
    },
    

 props: {
   
    source: String
  }
 
};



</script>

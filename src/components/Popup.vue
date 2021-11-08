<template>
  <v-row justify="center">
    <v-dialog v-model="dialog" persistent max-width="800px"> <!-- 경고창 -->
      <template v-slot:activator="{ on }"> <!-- on 은 액션창 생성 명령어 --> 
        <v-btn outlined color="white" dark v-on="on" > Register the Product </v-btn>
      </template>
      <v-card>
        <v-card-title>
          <span class="headline">상품 등록</span>
        </v-card-title>
         <v-form class="px-3" ref="form">
        <v-card-text>
           
                <v-text-field label="Title" v-model="title" prepend-icon="folder" :rules="inputRules"></v-text-field>
                <v-textarea label="Information" v-model="content" prepend-icon="edit" :rules="inputRules"></v-textarea>
                <v-col cols="12" lg="6">
                 <v-menu 
          ref="menu1"
          v-model="menu1"
          :close-on-content-click="false"
          transition="scale-transition"
          offset-y
          max-width="290px" 
          min-width="290px"
        > <!-- 달력 보이는 화면 290px 로 맞춤 -->
        
          <template v-slot:activator="{ on }"> <!-- 보증기간 선택 달력 -->
            <v-text-field
              v-model="dateFormatted"
              label="warranty"
              hint="상품 보증 기간을 입력해 주세요"
              persistent-hint
              prepend-icon="event"
              @blur="date = parseDate(dateFormatted)"
              v-on="on"
            ></v-text-field>
          </template>
          <v-date-picker v-model="date" no-title @input="menu1 = false"></v-date-picker>
        </v-menu>
        </v-col>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" text outlined @click="dialog = false">Close</v-btn>
          <v-btn color="green" text outlined @click="submit">Save</v-btn>
        </v-card-actions>
         </v-form>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<!-- 상품 등록할때 공백 등록 x , 최소 3글자 이상으로 하게 기본값 설정. script 부분 전체 -->
<script> 
export default {
    data: vm => ({
      dialog: false,
      title:'',
      content:'',
      due:null,
      date: new Date().toISOString().substr(0, 10),
      dateFormatted: vm.formatDate(new Date().toISOString().substr(0, 10)),
      menu1: false,
      inputRules: [
          v => v.length >= 3 || 'Minimum lenght is 3 charachters' 
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
}
</script>
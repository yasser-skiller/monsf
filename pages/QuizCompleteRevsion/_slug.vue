<template >
<div>
  <AppNav/>
  <div class="m-4" >
  <div v-if="this.Quiz_data.length > 0 ">
    <b-row align-h="center"  class="flex-wrap-reverse mb-5">
        <b-col cols="12" lg="6" class="m-sec">
          <p class="my-4 text_blue">الامتحان الالكتروني</p>
          <div class="rounded_0 bgGray p-3">
            <p class="text-center">السؤال الــ <span class="text_yellow">{{Quiz_serial+1}}</span> من السؤال الــ <span class="text_green">{{Quiz_data.length}}</span></p>
            <b-progress class="my-4">
              <b-progress-bar :value="(Quiz_serial+1)*100/Quiz_data.length"></b-progress-bar>
            </b-progress>
            <p>اختر من الإجابات التالية</p>
            <div class="Grid mt-5">
              <div
                v-for="option in Quiz_data[Quiz_serial].options"
                :key="option.uid"
                :id="option.value"
                :class="`class${option.value}`"
                v-on:click="Save(Quiz_data[Quiz_serial].id, option.value, Quiz_serial)"
              >
              <label
              :for="option.uid"
              >
              {{option.title}}
              </label>
              <b-form-radio
                v-model="selected"
                :id="`${option.uid}`"
                class="d-none"
                :value="option.value"
              >
              </b-form-radio>
            </div>
            </div>

            <div class="mt-3 ">Selected: <strong>{{ selected }}</strong></div>

          </div>
        </b-col>
        <b-col cols="12" lg="5" class="m-sec">

          <img :src="Quiz_data[Quiz_serial].thumbnail" class="thumbnail" alt="icon"/>


          <div
           class="d-flex bgfillRed border_red_2 px-3 py-2 mt-5 font-16 cursor_pointer"
           v-on:click="Favorite(Quiz_data[Quiz_serial])"
          >
            <span class="text_red">السؤال في المفضلة</span>
            <img :src="HeartCase === false ? require(`~/assets/icon/empatyHart.svg`) : require(`~/assets/icon/heart (10).svg`)" class="icon mr-auto" alt="icon"/>
          </div>

          <div
            class="d-flex bgfillBlue border_blue_2 px-3 py-2 mt-5 font-16 cursor_pointer"
            v-on:click="Pass(Quiz_data[Quiz_serial])"
          >
            <div>
              <img :src="require(`~/assets/icon/late.svg`)" class="icon ml-2" alt="icon"/>
              <span class="text_blue">تأجيل السؤال</span>
            </div>
            <img :src="PassCase === false ? require(`~/assets/icon/emptyBox.svg`) : require(`~/assets/icon/checkBox.svg`)" class="icon mr-auto" alt="icon"/>
          </div>


          <AddFoldersList :Quiz_data="Quiz_data" :Quiz_serial="Quiz_serial"/>


          <div class="my-5 d-flex flex-wrap justify-content-between">
            <b-button size="sm" class="btn btn_red my-2 py-2 px-r px-l rounded_0" type="button" v-if="Quiz_serial > 0 " v-on:click="Previous"> السابق</b-button>
            <b-button size="sm" class="btn btn_yellow my-2 py-2 px-r px-l rounded_0 mx-5" type="button" v-if="Quiz_serial !== Quiz_data.length-1 " v-on:click="Next"> التالي</b-button>
            <b-button size="sm" class="btn btn_yellow my-2 py-2 px-r px-l rounded_0 mx-auto" type="button"  v-on:click="Finish_Quiz">المراجعة</b-button>
          </div>

        </b-col>
    </b-row>
  </div>

  <div v-else class="d-flex justify-content-center align-items-center spinner_loading">
    <Loading/>
  </div>


  </div>
</div>

</template>

<script>
import Loading from "@/components/Loading";
import AppNav from '@/components/AppNav';
import AddFoldersList from "@/components/AddFoldersList";

  export default {
    components:{
      Loading,
      AppNav,
      AddFoldersList
    },
    data() {
      return {
        Quiz_data: [],
        Answered_obj : {},
        Answered:[],
        Favorite_Quiz:[],
        Pass_Quiz:[],
        Result:[],
        selected: '',
        status_code: '',
        Quiz_serial:0,
        Quiz_duration:0,
        Minute:0,
        Seconds:0,
        Remseconds:0,
        HeartCase: false,
        Favorite_Quiz :[],
        PassCase:false,
        Pass_Quiz :[],

      }
    },
    mounted() {
      this.CurrentState();
      setTimeout(() => {
        this.Compare();
      }, 2000);
    },
    methods: {
      CurrentState(){
        this.Pass_Quiz = JSON.parse(localStorage.getItem(`Pass_Quiz_${this.$route.params.slug}`));
        this.Favorite_Quiz = JSON.parse(localStorage.getItem(`Favorite_Quiz_${this.$route.params.slug}`));
        this.Result = JSON.parse(localStorage.getItem(`Result_${this.$route.params.slug}`));
        this.Answered = JSON.parse(localStorage.getItem(`Answered_${this.$route.params.slug}`));
        this.Result_ids = []

        console.log('localStorage.Result_',JSON.parse(localStorage.getItem(`Result_${this.$route.params.slug}`)))

        for (const property in this.Result.results.answered) {
          if(this.Result.results.answered[property].correct === true){
            console.log(`${property}`);
            this.Result_ids.push(parseInt(property))
          }

        }

        JSON.parse(localStorage.getItem(`Quiz_data_${this.$route.params.slug}`)).forEach(element => {
          this.Result_ids.forEach(ele => {
            if(element.id === ele){
             this.Quiz_data.push(element)
            }
          });

        });



        console.log('locQuiz_data_', this.Quiz_data)

      },
      Compare(){

        console.log("zzzzz",this.Answered)
        console.log("ooooozzz",this.Result.results)

        setTimeout(() => {
          if(this.Answered.length > 0){
          this.Answered.forEach(element => {
            if(element.id === this.Quiz_data[this.Quiz_serial].id){
              if(this.Result.results.answered[element.id].correct === true){
                // this.selected = element.answer
                document.querySelector(`.class${element.answer}`).classList.add('selected')
              }
              if(this.Result.results.answered[element.id].correct === false){
                this.Result.results.answered[element.id].options.forEach(ele => {
                  if(ele.is_true === 'yes'){
                    document.querySelector(`.class${ele.value}`).classList.add('selected')
                    // this.selected = ele.value
                  }
                });
                document.querySelector(`.class${this.Result.results.answered[element.id].answered.answered}`).classList.add('Wrongselected')

              }
            }else{
              this.Result.results.answered[this.Quiz_data[this.Quiz_serial].id].options.forEach(ele => {
                if(ele.is_true === 'yes'){
                  document.querySelector(`.class${ele.value}`).classList.add('selected')
                }
                if(ele.value === this.Result.results.answered[this.Quiz_data[this.Quiz_serial].id].answered.answered){
                  document.querySelector(`.class${ele.value}`).classList.add('Wrongselected')
                }
              });
            }
          });
        }

        }, 500);



      //Favorite
      this.HeartCase = false;
      this.Favorite_Quiz.forEach(element => {
        if(element.id === this.Quiz_data[this.Quiz_serial].id){
          this.HeartCase = true;
        }
      });

      //Pass
      this.PassCase = false;
      this.Pass_Quiz.forEach(element => {
        if(element.id === this.Quiz_data[this.Quiz_serial].id){
          this.PassCase = true;
        }
      });

      //FoldersListCheckbox
      document.querySelectorAll('.FoldersListCheckbox input').forEach(element => {
        element.checked = false
      });

    },
    Save(id, option_value, my_Quiz_serial){
      if(this.Answered.length > 0){
        this.Answered.forEach(element => {
          if(element){
            if(element.id === id){
              this.Answered =  this.Answered.filter(e => e !== element);
            }
          }
        });
        this.Answered.push({'id':id,'answer':option_value,'my_Quiz_serial':my_Quiz_serial});
      }if(this.Answered.length === 0){
        this.Answered.push({'id':id,'answer':option_value,'my_Quiz_serial':my_Quiz_serial});
      }


    },
    Next(){
      this.Quiz_serial++ ;
      this.Compare();
    },
    Pass(item){
      this.PassCase = !this.PassCase;
      if(this.PassCase === true){
        this.Pass_Quiz.push(item)
      }
      if(this.PassCase === false){
        console.log("Pass_Quiz false")
        this.Pass_Quiz =  this.Pass_Quiz.filter(e =>  e.id !== item.id)
      }
      console.log("Pass_Quiz",this.Pass_Quiz)
      console.log("item",item)
    },
    Previous(){
      this.Quiz_serial-- ;
      this.Compare();
    },
    Finish_Quiz(){
      console.log("localStorage_AnsweredvFinish_Quiz",this.Answered)
      localStorage.setItem(`Answered_${this.$route.params.slug}`, JSON.stringify(this.Answered));
      localStorage.setItem(`Quiz_duration${this.$route.params.slug}`, JSON.stringify((this.Minute*60)+this.Remseconds));
      localStorage.setItem(`Favorite_Quiz_${this.$route.params.slug}`, JSON.stringify(this.Favorite_Quiz));
      localStorage.setItem(`Pass_Quiz_${this.$route.params.slug}`, JSON.stringify(this.Pass_Quiz));
      this.$router.push({path:`/ResultsRevsion/${this.$route.params.slug}`});
    },
    Favorite(item){
      this.HeartCase = !this.HeartCase;
      if(this.HeartCase === true){
        this.Favorite_Quiz.push(item)
      }
      if(this.HeartCase === false){
        console.log("Favorite_Quiz false")
        this.Favorite_Quiz =  this.Favorite_Quiz.filter(e =>  e.id !== item.id)
      }
      console.log("Favorite_Quiz",this.Favorite_Quiz)
    },


  },


  }
</script>

<style scoped>
  .thumbnail{
    width: 100%;
    height: 150px;
  }
  .spinner_loading{
    height: 90vh;
  }
 .progress{
  background-color: #FFD89B;
  height: .5rem;
 }
 .progress-bar{
  background-color: #E99005;
 }
 .Grid{
   display: grid;
   grid-template-columns: auto auto ;
    row-gap: 30px;
 }
 .px-r{
  padding-right: 70px !important;
 }
 .px-l{
  padding-left: 70px !important;
 }
 .Grid div {
  border-radius: 50%;
  width: 70px;
  height: 70px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: bold;
  margin: auto;
  cursor: pointer !important;
 }
 .Grid div:first-child {
  border: #DB3A57 4px solid;
  color: #DB3A57;
 }
 .Grid div:nth-child(2) {
  border: #006490 4px solid;
  color: #006490;
 }
 .Grid div:nth-child(3) {
  border: #039A7B 4px solid;
  color: #039A7B;
 }
 .Grid div:nth-child(4) {
  border: #6B7377 4px solid;
  color: #6B7377;
 }
 label{
  cursor: pointer !important;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
 }

 .Wrongselected{
  outline: 2px solid rgb(221, 15, 15);
  outline-offset: 5px;
 }

 .selected{
  outline: 2px solid rgb(15, 192, 124);
  outline-offset: 5px;
 }





</style>

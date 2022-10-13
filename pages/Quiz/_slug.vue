<template>
  <div>
    <AppNav/>
    <b-container>
      <div v-if="status_code === 'success' && this.Quiz_data.length > 0 ">
        <b-row align-h="center"  class="flex-wrap-reverse mb-5">
          <b-col cols="12" lg="6" class="m-sec">
            <div class="d-flex flex-wrap">
              <div class="border rounded_0 fit_width bg_GraySec py-1 px-2 ml-3">
                <img :src="require(`~/assets/icon/clockTimer.svg`)" class="" alt="icon"/>
                <span class="text_blue font-16 px-2">{{Quiz_duration}}</span>
              </div>

              <div class="d-flex align-items-center" v-if="Minute < 5 ">
                <img :src="require(`~/assets/icon/attention.svg`)" class="" alt="icon"/>
                <p class="text-danger mr-2 my-0 font-weight-bold">الوقت أوشك علي الأنتهاء </p>
              </div>
            </div>


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
                  :class="selected === option.value ? `selected` : ``"
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

              <!-- <div class="mt-3 ">Selected: <strong>{{ selected }}</strong></div> -->

            </div>
          </b-col>
          <b-col cols="12" lg="5" class="m-sec ">

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

            <div class="my-5 d-flex justify-content-between">
              <b-button size="sm" class="btn btn_red my-2 py-2 px-r px-l rounded_0" type="button" v-if="Quiz_serial > 0 " v-on:click="Previous"> السابق</b-button>
              <b-button size="sm" class="btn btn_yellow my-2 py-2 px-r px-l rounded_0 " type="button" v-if="Quiz_serial !== Quiz_data.length-1 " v-on:click="Next"> التالي</b-button>
              <b-button size="sm" class="btn btn_yellow my-2 py-2 px-r px-l rounded_0 " type="button" v-if="Quiz_serial === Quiz_data.length-1 " v-on:click="Finish_Quiz">إنهاء الاختبار</b-button>
            </div>

          </b-col>
        </b-row>
      </div>
      <div v-else class="d-flex justify-content-center align-items-center spinner_loading">
        <Loading/>
      </div>
    </b-container>
  </div>

</template>

<script>
 import config from "@/config";
 import AppNav from "@/components/AppNav";
 import Loading from "@/components/Loading";
 import AddFoldersList from "@/components/AddFoldersList";

 export default {
  components:{
    Loading,
    AppNav,
    AddFoldersList,
  },
  data (){
    return {
      Quiz_data: [],
      Answered_obj : {},
      selected : '',
      status_code: '',
      Quiz_duration: 0,
      Minute: 0,
      Seconds: 0,
      Remseconds: 0,
      Quiz_serial: 0,
      Answered : [],
      HeartCase: false,
      Favorite_Quiz :[],
      PassCase:false,
      Pass_Quiz :[],
    }
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      var myHeaders = new Headers();
      myHeaders.append("Authorization", `Bearer${config.token}`);
      myHeaders.append("Content-Type", "application/json");

      var raw = JSON.stringify({"id":this.$route.params.slug});

      var requestOptions = {
        method: 'POST',
        headers: myHeaders,
        body: raw,
        redirect: 'follow'
      };

      fetch(config.apiUrl+"wp-json/learnpress/v1/quiz/start", requestOptions)
      .then(response => response.text())
      .then(res => {
        console.log(JSON.parse(res))
        this.Quiz_data = JSON.parse(res).results.questions;
        this.Seconds =  JSON.parse(res).results.duration;
        this.status_code = JSON.parse(res).status;
      })
      .catch (error => console.log(error));
    },
    Next(){
      this.Quiz_serial++ ;
      this.Compare();
    },
    Previous(){
      this.Quiz_serial-- ;
      this.Compare();
    },
    Finish_Quiz(){
      localStorage.setItem(`Answered_${this.$route.params.slug}`, JSON.stringify(this.Answered));
      localStorage.setItem(`Quiz_data_${this.$route.params.slug}`, JSON.stringify(this.Quiz_data));
      localStorage.setItem(`Favorite_Quiz_${this.$route.params.slug}`, JSON.stringify(this.Favorite_Quiz));
      localStorage.setItem(`Pass_Quiz_${this.$route.params.slug}`, JSON.stringify(this.Pass_Quiz));
      this.$router.push({path:`/Result/${this.$route.params.slug}`})
    },
    Compare(){
      if(this.Answered.length > 0){
        this.Answered.forEach(element => {
          if(element.my_Quiz_serial === this.Quiz_serial){
            this.selected = element.answer
          }
        });
      }

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
        console.log("this.Answered",this.Answered)
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
    SendData() {
        var myHeaders = new Headers();
        myHeaders.append("Authorization", `Bearer${config.token}`);
        myHeaders.append("Content-Type", "application/json");

        if(this.Answered.length > 0){
          for (var i=0; i<this.Answered.length; i++){
            this.Answered_obj[this.Answered[i].id] = {answered: `${this.Answered[i].answer}`} ;
          }
        }

        var raw = JSON.stringify({"id":this.$route.params.slug, "answered" : this.Answered_obj});

        var requestOptions = {
          method: 'POST',
          headers: myHeaders,
          body: raw,
          redirect: 'follow'
        };

        fetch(config.apiUrl+"wp-json/learnpress/v1/quiz/finish", requestOptions)
          .then(response => response.text())
          .then(res => {
            localStorage.setItem(`Result_${this.$route.params.slug}`, res);
            this.$router.push({path:`/TestResults/${this.$route.params.slug}`})
          })
          .catch(error => console.log('error', error));
    },
  },
  watch: {
      Seconds: {
        handler(value) {
          if (value > 0) {
            setTimeout(() => {
              this.Minute = Math.floor(this.Seconds / 60)
              this.Remseconds = this.Seconds % 60
              this.Seconds--;
              if(this.Seconds < 9){
                this.Quiz_duration = this.Minute + ':0' + this.Remseconds
              }if(this.Minute < 9){
                this.Quiz_duration = "0"+this.Minute + ':' + this.Remseconds
              }else{
                this.Quiz_duration = this.Minute + ':' + this.Remseconds
              }
              localStorage.setItem(`Quiz_duration${this.$route.params.slug}`, JSON.stringify((this.Minute*60)+this.Remseconds));
              if(this.Minute === 0 && this.Remseconds === 1){
                this.SendData();
              }
            }, 1000);

          }
        },
        immediate: true,
      },

  }
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
 .selected{
  outline: 2px solid rgb(15, 192, 124);
  outline-offset: 5px;
 }


</style>

<template>
  <div>
      <AppNav/>
    <b-container class="my-4" >
      <div v-if="this.Answered.length > 0  ">
        <div class="mb-sec">.</div>
        <b-row  align-h="center"  class="flex-wrap  justify-content-between align-items-center bg-DarkBlueOldColor p-1">
          <b-col cols="11" sm="10"  md="8" lg="6" class="">
            <p class="m-0">اسم الاختبار- اسم المختبر</p>
          </b-col>
          <b-col cols="11" sm="10"  md="8" lg="6" class="d-flex flex-column align-items-end">
            <p class="m-0 f-12">
              <img :src="require(`~/assets/icon/clock.svg`)" alt="img" class="clock_img"/>
            الوقت المتبقي : {{Quiz_duration}}</p>
          </b-col>
        </b-row>

        <b-row  align-h="center"  class="my-4 flex-wrap justify-content-between align-items-center">
          <b-col cols="11" sm="10"  md="4" lg="4" class="mx-auto" v-b-modal.modal-5 v-on:click="CheckPassQuiz">
            <div class="parent" >
              <img :src="require(`~/assets/img/Group 1483.png`)" alt="img" class="w-100"/>
              <div class="overly font-16 font-weight-bold">
                <h5>{{Pass_Quiz.length}}</h5>
                <div class="d-flex mt-5 ml-auto">
                  <img :src="require(`~/assets/icon/folder4.svg`)" alt="img" class="icon"/>
                  <p class="my-0 mr-2">الأسئلة المؤجلة</p>
                </div>
              </div>
            </div>
          </b-col>

          <b-col cols="11" sm="10"  md="4" lg="4" class="mx-auto" v-b-modal.modal-6 v-on:click="CheckQuizIncomplete">
            <div class="parent">
              <img :src="require(`~/assets/img/Group 1484.png`)" alt="img" class="w-100"/>
              <div class="overly font-16 font-weight-bold">
                <h5>{{Quiz_data.length - Answered.length}}</h5>
                <div class="d-flex mt-5 ml-auto">
                  <img :src="require(`~/assets/icon/late0.svg`)" alt="img" class="icon"/>
                  <p class="my-0 mr-2"> الأسئلة الغير محلولة</p>
                </div>
              </div>
            </div>
          </b-col>

          <b-col cols="11" sm="10"  md="4" lg="4" class="mx-auto" v-b-modal.modal-4 v-on:click="CheckQuizComplete">
            <div class="parent">
              <img :src="require(`~/assets/img/Group 1485.png`)" alt="img" class="w-100"/>
              <div class="overly font-16 font-weight-bold">
                <h5>{{Answered.length}}</h5>
                <div class="d-flex mt-5 ml-auto">
                  <img :src="require(`~/assets/icon/heart (12).svg`)" alt="img" class="icon"/>
                  <p class="my-0 mr-2"> الأسئلة المحلولة</p>
                </div>
              </div>
            </div>
          </b-col>
        </b-row>

        <div class="text-center font-16">
          <p>تفاصيل الامتحان الالكتروني</p>
          <p class="my-4">اجمالي أسئلة الامتحان هما {{Quiz_data.length}} سؤال</p>
          <div class="d-flex justify-content-center">
            <div class="bgfillGreen py-2 border_Green_3 text_green">اسئلة محلولة {{Answered.length}} </div>
            <div class="bgfillBlue py-2 border_blue_3 text_blue mx-3">أسئلة مؤجلة {{Pass_Quiz.length}} </div>
            <div class="bgfillRed py-2 border_red_3 text_red">أسئلة غير محلولة  {{Quiz_data.length - Answered.length}} </div>

          </div>
        </div>

        <div class="mt-5 d-flex justify-content-center">
          <b-button v-on:click="CheckRevsionQuiz" size="sm" class="btn btn_blue my-2 py-3 px-5 rounded_0 ml-5" type="button"> مراجعة الكل</b-button>
          <b-button v-on:click="SendData" size="sm" class="btn btn_Green my-2 py-3 px-5 rounded_0" type="button"> تسليم الامتحان</b-button>

        </div>


        <b-modal id="modal-4" title="قسم المراجعة" hide-footer>
          <p>لا يوجد أسئلة غير مكتملة</p>
        </b-modal>

        <b-modal id="modal-5" title="قسم المراجعة" hide-footer>
          <p>لا يوجد أسئلة  مؤجلة</p>
        </b-modal>

        <b-modal id="modal-6" title="قسم المراجعة" hide-footer>
          <p>لا يوجد أسئلة  ممحلولة</p>
        </b-modal>


      </div>
      <div v-else class="d-flex justify-content-center align-items-center spinner_loading">
        <Loading/>
      </div>
    </b-container>


  </div>
</template>

<script>
import config from "@/config";
import AppNav from '@/components/AppNav';
import Loading from "@/components/Loading";

  export default {
    components:{
      Loading,
      AppNav,
    },
    data() {
      return {
        Answered:[],
        Result:[],
        Quiz_data:[],
        Pass_Quiz :[],
        Answered_obj : {},
        selected: '',
        status_code: '',
        Quiz_serial:0,
        Quiz_duration:0,
        Minute:0,
        Seconds:0,
        Remseconds:0,
        Incompleted_Answered:[],
      }
    },
    mounted() {
      console.log('localStorage.Pass_Quiz_',JSON.parse(localStorage.getItem(`Pass_Quiz_${this.$route.params.slug}`)))
      console.log('localStorage.Quiz_duration',JSON.parse(localStorage.getItem(`Quiz_duration${this.$route.params.slug}`)))
      console.log('localStorage.Answered_',JSON.parse(localStorage.getItem(`Answered_${this.$route.params.slug}`)))
      console.log('localStorage.Quiz_data_',JSON.parse(localStorage.getItem(`Quiz_data_${this.$route.params.slug}`)))
      this.Answered = JSON.parse(localStorage.getItem(`Answered_${this.$route.params.slug}`));
      this.Quiz_data = JSON.parse(localStorage.getItem(`Quiz_data_${this.$route.params.slug}`));
      this.Pass_Quiz = JSON.parse(localStorage.getItem(`Pass_Quiz_${this.$route.params.slug}`));
      this.Seconds = JSON.parse(localStorage.getItem(`Quiz_duration${this.$route.params.slug}`));
    },
    methods: {
      CheckQuizIncomplete(){
        if(this.Quiz_data.length - this.Answered.length > 0){
          this.$router.push({path:`/QuizIncomplete/${this.$route.params.slug}`})
        }
      },
      CheckQuizComplete(){
        if(this.Answered.length > 0){
          this.$router.push({path:`/QuizComplete/${this.$route.params.slug}`})
        }
      },
      CheckRevsionQuiz(){
        localStorage.removeItem(`Quiz_serial${this.$route.params.slug}`);
        this.$router.push({path:`/QuizRevsion/${this.$route.params.slug}`})
      },
      CheckPassQuiz(){
        if(this.Pass_Quiz.length > 0){
          this.$router.push({path:`/CheckPassQuiz/${this.$route.params.slug}`})
        }

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
            console.log('finisf',JSON.parse(res))
            this.status_code = JSON.parse(res).status;
            this.Result = [JSON.parse(res).results];
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
            }, 1000);
            if(this.Minute === 0 && this.Remseconds === 1){
              this.$router.push({path:`/Result/${this.$route.params.slug}`})
            }
          }
        },
        immediate: true,
      },

    }

  }
</script>


<style scoped>

.spinner_loading{
  height: 90vh;
}
.selected{
  border: 2px solid var(--BlueColor);
}

.clock_img{
  width: 22px;
  margin-left: 2px;
}
.parent{
  position: relative;
  cursor: pointer;
}
.overly{
  position:absolute ;
  top: 70px;
  right: 0;
  left: 0;
  bottom: 0;
  color: #fff;
  padding: 9px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.icon{
  width: 20px;
}
</style>

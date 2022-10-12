<template>
  <div>
    <b-alert v-if="Minute > 4 ? '' : 'd-none'" show  dismissible variant="danger">أوشك الوقت علي الأنتهاء لديك أقل من 5 دقائق</b-alert>
      <AppNav/>
    <b-container class="" >
      <div v-if="this.Quiz_data.length > 0  ">
        <b-row  align-h="center">
          <div class="mt-5">.</div>
          <div class="d-flex flex-wrap w-100 p-2 justify-content-between align-items-center bg-DarkBlueOldColor p-1">
          <b-col cols="11" sm="10"  md="6" lg="6" class="">
            <p class="m-0">اسم الاختبار- اسم المختبر</p>
          </b-col>
          <b-col cols="11" sm="10"  md="6" lg="6" class=" d-flex flex-column align-items-end">
            <p :class="Minute > 4 ? 'm-0 f-12 text-white' : 'm-0 f-12 text-danger' ">
              <img :src="require(`~/assets/icon/clock.svg`)" alt="img" class="clock_img"/>
            الوقت المتبقي : {{Quiz_duration}}</p>
            <p class="m-0 f-12 mt-1">السؤال  <span class="">{{Quiz_serial+1}}</span> من <span class="">{{Quiz_data.length}}</span> سؤال</p>
          </b-col>
        </div>
        </b-row>

        <h5 class="text-center my-3">قسم المراجعة</h5>
        <div class="bg-BlueOldColor p-2">
          <p class="m-0 text-white">إرشادات</p>
        </div>
        <div>
          <p>فيما يلي ملخص لإجابتك يمكنك مراجعة أسئلتك بثلاث (3) طرق مختلفة</p>
          <p>الأزرار الموجودة في الركن السفلي الأيسر تطابق هذه الخيارات:</p>
          <ul>
            <li>قم بمراحعة كل أسئلتك و إجاباتك </li>
            <li>قم بمراجعة أسئلتك الغير مكتملة</li>
            <li>قم بمراجعة الأسئلة المميزة بعلامة المراجعة</li>
          </ul>
          <P>يمكنك ايضا النقر فوق رقم سؤال لربطه مباشرة بموقعه في الاختبار</P>
        </div>
        <div class="bg-BlueOldColor p-2">
          <p class="m-0 text-white">الباب 1 جزء</p>
        </div>


        <div class="grid-container  w-100 mt-5 mb-4">
          <div class="border_0000" v-for="(item, index) in All" :key="index">
          <span
            class="Pagination_label d-flex justify-content-between p-1"
            >
            <div v-on:click="CheckRevsionQuestion(index)">
              <img  v-if="item.Pass === false" :src="require(`~/assets/icon/flag_unmarked.svg`)" alt="img" class="clock_img ml-1"/>
              <img v-if="item.Pass === true" :src="require(`~/assets/icon/flag_marked.svg`)" alt="img" class="clock_img ml-1"/>
              سؤال {{index +1}}
            </div>

            <p v-if="item.Answered === false " class="text-danger ml-2">غير مكتمل</p>
            </span>
          </div>
        </div>

        <b-row  align-h="center"  class="flex-wrap  justify-content-between align-items-center bg-DarkBlueOldColor py-1">
          <b-col cols="11" sm="10"  md="3" lg="2" class="">
            <p v-on:click="SendData" class="cursor_pointer m-0">الأنتهاء من الأسئلة</p>
          </b-col>
          <b-col cols="11" sm="10"  md="3" lg="2" class="">
          </b-col>
          <b-col cols="11" sm="10"  md="3" lg="2" class="">
            <span v-on:click="CheckRevsionQuiz" class="cursor_pointer m-0">مراجعة الكل</span>
          </b-col>
          <b-col cols="11" sm="10"  md="3" lg="2" class="">
            <span  v-b-modal.modal-4 v-on:click="CheckQuizIncomplete" class="cursor_pointer m-0">مراجعة الغير مكتمل</span>
          </b-col>
          <b-col cols="11" sm="10"  md="3" lg="2" class="">
            <span  v-b-modal.modal-5 v-on:click="CheckQuizMarked" class="cursor_pointer m-0">مراجعة المميز بعلامة</span>
          </b-col>
        </b-row>


        <b-modal id="modal-4" title="قسم المراجعة" hide-footer>
          <p>لا يوجد أسئلة غير مكتملة</p>
        </b-modal>

        <b-modal id="modal-5" title="قسم المراجعة" hide-footer>
          <p>لا يوجد أسئلة مميزة بعلامة</p>
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
        Pass_Quiz: [],
        Quiz_data:[],
        Answered_obj : {},
        selected: '',
        status_code: '',
        Quiz_serial:0,
        Quiz_duration:0,
        Minute:5,
        Seconds:0,
        Remseconds:0,
        Incompleted_Answered:[],
        All:[],
        Answered_obj :{},

      }
    },
    mounted() {
      console.log('localStorage.Quiz_duration',JSON.parse(localStorage.getItem(`Quiz_duration${this.$route.params.slug}`)))
      console.log('localStorage.',JSON.parse(localStorage.getItem(`Answered_${this.$route.params.slug}`)))
      console.log('localStorage.',JSON.parse(localStorage.getItem(`Quiz_data_${this.$route.params.slug}`)))
      this.Answered = JSON.parse(localStorage.getItem(`Answered_${this.$route.params.slug}`));
      this.Quiz_data = JSON.parse(localStorage.getItem(`Quiz_data_${this.$route.params.slug}`));
      this.Pass_Quiz = JSON.parse(localStorage.getItem(`Pass_Quiz_${this.$route.params.slug}`));
      this.Seconds = JSON.parse(localStorage.getItem(`Quiz_duration${this.$route.params.slug}`));
      this.Made();
    },
    methods: {
      Made(){
        this.Answered_ids = [];
        this.Pass_Quiz_ids = [];

        this.Answered.forEach(element => {
          this.Answered_ids.push(element.id);
        });

        this.Pass_Quiz.forEach(element => {
          this.Pass_Quiz_ids.push(element.id);
        });

        this.Quiz_data.forEach(ele => {
          this.All.push({ele,Answered:false, Pass:false});
        });

        this.All.forEach(element => {
          if(this.Answered_ids.includes(element.ele.id)){
            element.Answered = true
          }
          if(this.Pass_Quiz_ids.includes(element.ele.id)){
            element.Pass = true
          }
        });

      },
      CheckQuizIncomplete(){
        if(this.Quiz_data.length - this.Answered.length > 0){
          this.$router.push({path:`/OldStyleQuizIncomplete/${this.$route.params.slug}`})
        }
      },
      CheckQuizMarked(){
        if(this.Pass_Quiz.length > 0){
          this.$router.push({path:`/OldStyleQuizMarked/${this.$route.params.slug}`})
        }
      },
      CheckRevsionQuiz(){
        localStorage.removeItem(`Quiz_serial${this.$route.params.slug}`);
        this.$router.push({path:`/OldStyleRevsionQuiz/${this.$route.params.slug}`})
      },
      CheckRevsionQuestion(serial){
        this.$router.push({path:`/OldStyleRevsionQuiz/${this.$route.params.slug}`})
        localStorage.setItem(`Quiz_serial${this.$route.params.slug}`, JSON.stringify(serial));
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
            localStorage.setItem(`page_${this.$route.params.slug}`, 'old');
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

.spinner_loading{
  height: 90vh;
}
.selected{
  border: 2px solid var(--BlueColor);
}
.Pagination_label{
  cursor: pointer;
  color: var(--DarkWhiteSceColor);
}
.ImgManger{
  max-height: 400px;
  width: 100%;
}
.box{
  width: 20px;
  height: 20px;
}
.Responsive4{
  display: grid;
  grid-template-columns: auto auto ;
  align-items: flex-start;
  grid-column-gap: 25px;
}
.Responsive{
  display: grid;
  grid-template-columns: auto  ;
}
.clock_img{
  width: 22px;
  margin-left: 2px;
}
.grid-container {
  display: grid;
  grid-template-columns: auto auto auto auto auto;
}
</style>

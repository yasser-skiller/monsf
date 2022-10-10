<template>
  <div>
    <AppNav/>
    <b-container class="" >
      <div v-if="this.Quiz_data.length > 0  ">
        <div class="mb-sec">.</div>
        <b-row  align-h="center"  class="flex-wrap  justify-content-between align-items-center p-1">
          <b-col cols="11" sm="10"  md="8" lg="6" class="">
            <p class="m-0 font-weight-bold text_blue font-16">مراجعة الامتحان</p>
          </b-col>
          <b-col cols="11" sm="10"  md="8" lg="6" class="d-flex flex-column align-items-end">
          </b-col>
        </b-row>


        <b-row  align-h="center"  class="my-4 flex-wrap justify-content-between align-items-center">

          <b-col cols="11" sm="10"  md="3" lg="3" class="mx-auto" v-b-modal.modal-4 v-on:click="CheckQuizComplete">
            <div class="parent">
              <img :src="require(`~/assets/icon/question1.svg`)" alt="img" class=""/>
              <p class="my-0 font-16">  عدد الأسئلة المحلولة</p>
              <h4 class="text_blue font-weight-bold">{{Answered.length}}</h4>
            </div>
          </b-col>

          <b-col cols="11" sm="10"  md="3" lg="3" class="mx-auto" >
            <div class="parent">
              <img :src="require(`~/assets/icon/question (4).svg`)" alt="img" class=""/>
              <p class="my-0 font-16">   عدد الأسئلة الغير المحلولة</p>
              <h4 class=" font-weight-bold">{{Quiz_data.length - Answered.length}}</h4>
            </div>
          </b-col>

          <b-col cols="11" sm="10"  md="3" lg="3" class="mx-auto" >
            <div class="parent" >
              <img :src="require(`~/assets/icon/survey.svg`)" alt="img" class=""/>
              <p class="my-0 font-16"> عدد الأسئلة المؤجلة</p>
              <h4 class=" font-weight-bold">{{Pass_Quiz.length}}</h4>
            </div>
          </b-col>

          <!-- <b-col cols="11" sm="10"  md="3" lg="3" class="mx-auto" v-b-modal.modal-7 v-on:click="CheckFavorite">
            <div class="parent">
              <img :src="require(`~/assets/icon/quiz2.svg`)" alt="img" class=""/>
              <p class="my-0 font-16">عدد الأسئلة المضافة للمفضلة</p>
              <h4 class="text_dark">{{Favorite_Quiz.length}}</h4>
            </div>
          </b-col> -->

        </b-row>

        <div class="itemsParent">
          <p>    مراجعة الأسئلة محلولة</p>
          <div class="d-flex my-4">
            <p class="my-0 mt-2">المراجع الان:<span class="font-weight-bold text_orange bgfillOrange rounded px-3 py-2 mx-2">{{FinishNum}}</span>من <span class="font-weight-bold bgfillGrag rounded px-3 py-2 mx-2">{{Answered.length}}</span></p>
            <img :src="require(`~/assets/icon/Group 2273.svg`)" alt="" class="mx-4" v-on:click="NextGroup"/>
            <img :src="require(`~/assets/icon/Group 2274.svg`)" alt="" class="" v-on:click="PerGroup"/>
          </div>

          <div class="items" >
            <div class="item  cursor_pointer" v-for="(item, index) in All_Modfiy" :key="index" v-on:click="CheckRevsionQuizItem(index)">
              <span class="font-weight-bold">({{index+StartNum+1}})</span>
              <div class="mr-auto">
                <span  class="span Answered ml-2">سؤال محلول</span>
              </div>

            </div>
          </div>

        </div>

        <div class="mt-5 d-flex justify-content-center">
          <b-button v-on:click="$router.push({path:`/TestResults/${$route.params.slug}`})" size="sm" class="btn btn_blue my-2 py-3 px-5 rounded_0 mx-auto" type="button"> العودة للنتائج</b-button>

        </div>


        <b-modal id="modal-6" title="قسم المراجعة" hide-footer>
          <p>لا يوجد أسئلة غير ممحلولة</p>
        </b-modal>


      </div>
      <div v-else class="d-flex justify-content-center align-items-center spinner_loading">
        <Loading/>
      </div>
    </b-container>
  </div>
</template>

<script>
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
        Incompleted_Answered:[],
        StartNum: 0,
        FinishNum: 9,
        // All:[],
        All_Modfiy:[],
      }
    },
    mounted() {
      console.log('localStorage.Pass_Quiz_',JSON.parse(localStorage.getItem(`Pass_Quiz_${this.$route.params.slug}`)))
      console.log('localStorage.Quiz_duration',JSON.parse(localStorage.getItem(`Quiz_duration${this.$route.params.slug}`)))
      console.log('localStorage.Answered_',JSON.parse(localStorage.getItem(`Answered_${this.$route.params.slug}`)))
      console.log('localStorage.Quiz_data_',JSON.parse(localStorage.getItem(`Quiz_data_${this.$route.params.slug}`)))
      this.Result = JSON.parse(localStorage.getItem(`Result_${this.$route.params.slug}`));
      this.Answered = JSON.parse(localStorage.getItem(`Answered_${this.$route.params.slug}`));
      this.Quiz_data = JSON.parse(localStorage.getItem(`Quiz_data_${this.$route.params.slug}`));
      this.Pass_Quiz = JSON.parse(localStorage.getItem(`Pass_Quiz_${this.$route.params.slug}`));
      this.Made();
    },
    methods: {
      Made(){
        // this.Answered_ids = [];
        // this.Pass_Quiz_ids = [];
        // this.Favorite_Quiz_ids = [];

        // this.Answered.forEach(element => {
        //   this.Answered_ids.push(element.id);
        // });

        // this.Pass_Quiz.forEach(element => {
        //   this.Pass_Quiz_ids.push(element.id);
        // });

        // this.Favorite_Quiz.forEach(element => {
        //   this.Favorite_Quiz_ids.push(element.id);
        // });

        // this.Quiz_data.forEach(ele => {
        //   this.All.push({ele,Answered:false, Favorite:false, Pass:false});
        // });

        // this.All.forEach(element => {
        //   if(this.Answered_ids.includes(element.ele.id)){
        //     element.Answered = true
        //   }
          // if(this.Favorite_Quiz_ids.includes(element.ele.id)){
          //   element.Favorite = true
          // }
          // if(this.Pass_Quiz_ids.includes(element.ele.id)){
          //   element.Pass = true
          // }
        // });

        this.All_Modfiy = this.Answered.slice(this.StartNum,this.FinishNum);

        if(this.FinishNum > this.Answered.length){
          this.FinishNum = this.Answered.length
        }
      },
      NextGroup(){
        if(this.FinishNum < this.Answered.length){
          this.StartNum = this.StartNum + 9 ;
          this.FinishNum = this.FinishNum + 9 ;
        }
        if(this.FinishNum > this.Answered.length){
          this.FinishNum = this.Answered.length ;

        }
        if(this.FinishNum = this.Answered.length){
          this.FinishNum = this.Answered.length ;

        }
        this.All_Modfiy = this.Answered.slice(this.StartNum,this.FinishNum)

      },
      PerGroup(){

        if(this.StartNum !== 0){
          if(this.FinishNum === this.Answered.length){
            this.FinishNum =  this.StartNum ;
            this.StartNum = this.StartNum - 9 ;
          }else{
            this.StartNum = this.StartNum - 9 ;
            this.FinishNum = this.FinishNum - 9 ;
          }

        }

        this.All_Modfiy = this.Answered.slice(this.StartNum,this.FinishNum)

      },
      CheckQuizComplete(){
        if(this.Answered.length > 0){
          this.$router.push({path:`/QuizCompleteRevsion/${this.$route.params.slug}`})
        }
      },
      CheckRevsionQuizItem(Quiz_serial){
        localStorage.setItem(`Quiz_serial${this.$route.params.slug}`, JSON.stringify(Quiz_serial));
        this.$router.push({path:`/QuizCompleteRevsion/${this.$route.params.slug}`})
      },

    },
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
.parent{
  position: relative;
  cursor: pointer;
  width: 100%;
  height: 200px;
  background-color: #F3F4F6;
  border: 2px solid #EFF0F3;
  border-radius: 20px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;

}
.itemsParent{
  background-color: #FBFBFB;
  border: 1px solid #C4C4C4;
  padding: 20px;
  border-radius: 20px;
}
.items{

  display: grid;
  grid-template-columns: auto auto auto;
  grid-column-gap: 20px;
  grid-row-gap: 20px;
}
.item{
  background-color: #F2F3F9;
  border-radius: 15px;
  padding: 15px;
  display: flex;
  justify-content: space-between;
  width: 100%;

}
.span{
  border-radius: 10px;
  padding: 10px;
}
.Answered{
  color: #48AB70;
  background-color: #BBEBCE;
}
.unAnswered{
  color: #BC2022;
  background-color: #F1BDBD;
}
.Pass{
  color: #2A508D;
  background-color: #D1D8E3;
}
</style>

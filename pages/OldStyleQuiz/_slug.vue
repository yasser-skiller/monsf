<template >
<div >
  <b-alert v-if="Minute > 4 ? '' : 'd-none'" show  dismissible variant="danger">أوشك الوقت علي الأنتهاء لديك أقل من 5 دقائق</b-alert>

  <AppNav/>
  <div class="">
    <div v-if="status_code === 'success' && this.Quiz_data.length > 0">

      <b-row  align-h="center"  class="">
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

      <b-row class="flex-wrap align-items-center  justify-content-end  bg-BlueOldColor p-1">
        <p class="cursor_pointer text-white m-0 ml-5"  v-on:click="Pass(Quiz_data[Quiz_serial])"><img :src="marked_case === false ? require(`~/assets/icon/flag_top.svg`) :  require(`~/assets/icon/flag_marked.svg`)" alt="img" class="clock_img"/> تميز السؤال للمراجعة </p>
        <b-dropdown id="dropdown-1" text="الخط" class="m-0 mr-5">
          <b-dropdown-item active>خط عادي</b-dropdown-item>
          <b-dropdown-item>خط عريض </b-dropdown-item>
          <b-dropdown-item>خط عريض بزياده</b-dropdown-item>
        </b-dropdown>
      </b-row>


        <b-row align-h="center"  class="px-3 align-items-start border sp_style">
          <b-col cols="11" sm="10"  md="8" lg="6" class="border_left pt-3">
            <b-row align-h="center"  class="flex-column flex-wrap justify-content-end pr-3 ">
              <b-col cols="11" sm="10"  md="8" lg="6">
                <div class="">
                    <img :src="Quiz_data[Quiz_serial].thumbnail" alt="img" class="rounded ImgManger"/>
                </div>
              </b-col>
              <b-col :class="Quiz_data[Quiz_serial].thumbnail ? 'min_height col-11 col-lg-6 col-md-8 col-sm-6 px-3 my-4' : 'col-11 px-3 my-4 min_height'">
                <b-form-group  v-slot="{ ariaDescribedby }">
                  <div :class="Quiz_data[Quiz_serial].thumbnail ? 'Responsive' : 'Responsive4' ">
                    <div
                      v-for="option in Quiz_data[Quiz_serial].options"
                      :key="option.uid"
                        v-on:click="Save(Quiz_data[Quiz_serial].id, option.value, Quiz_serial )"
                        class="radioParent"
                      >
                        <b-form-radio
                          :value="option.value"
                          v-model="selected"
                          :aria-describedby="ariaDescribedby"
                          :id="`${option.uid}`"
                        >
                        {{option.title}}
                        </b-form-radio>
                    </div>
                  </div>

                </b-form-group>

                <!-- <div class="mt-3 ">Selected: <strong>{{ selected }}</strong></div> -->

              </b-col>
            </b-row>
          </b-col>

          <b-col cols="11" sm="10"  md="8" lg="6" class="text-center pt-3">
            <h5>أسئلة اختيار من متعدد</h5>
            <h6>فيما يلي سؤال يتبعه أربعة اختيارات</h6>
            <p>المطلوب اختيار الاجابة الصحيحية</p>

          </b-col>
        </b-row>

        <b-row  align-h="center"  class="flex-wrap  justify-content-between align-items-center bg-DarkBlueOldColor p-1">
          <b-col cols="4" sm="4" class="">
            <p class="m-0">المعادلات</p>
          </b-col>
          <b-col cols="8" sm="8"  class="d-flex justify-content-end">
            <div v-if="Quiz_serial > 0 "  v-on:click="Previous" class="cursor_pointer ml-2"><img :src="require(`~/assets/icon/arrow_right.svg`)" alt="img" class="clock_img ml-2"/>السابق</div>
            <div  v-if="Quiz_serial !== Quiz_data.length-1 " v-on:click="Next" class="cursor_pointer f-18">التالي<img :src="require(`~/assets/icon/arrow_left.svg`)" alt="img" class="clock_img mr-2"/></div>
            <div class="mr-2 cursor_pointer f-18"  v-if="Quiz_serial === Quiz_data.length-1 " v-on:click="Finish_Quiz">الأنتهاء من الأسئلة</div>
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
import config from "@/config";
import Loading from "@/components/Loading";
import AppNav from '@/components/AppNav';

  export default {
    components:{
      Loading,
      AppNav
    },
    data() {
      return {
        Quiz_data: [],
        Answered:[],
        Pass_Quiz :[],
        Answered_obj:{},
        selected: '',
        status_code: '',
        Quiz_serial:0,
        Quiz_duration:0,
        Minute:5,
        Seconds:0,
        Remseconds:0,
        Delay_Qu : false,
        marked_case:false,
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
          this.Quiz_data = JSON.parse(res).results.questions;
          this.Seconds =  JSON.parse(res).results.duration;
          this.status_code = JSON.parse(res).status;
        })
        .catch (error => console.log(error));
      },
      Compare(){
        if(this.Answered.length > 0){
        this.Answered.forEach(element => {
          if(element.my_Quiz_serial === this.Quiz_serial){
            this.selected = element.answer
          }
        });
      }


        //Pass
        this.marked_case = false;
        this.Pass_Quiz.forEach(element => {
          if(element.id === this.Quiz_data[this.Quiz_serial].id){
            this.marked_case = true;
          }
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
      Next(){
        this.Quiz_serial++ ;
        this.Compare();
      },
      Pass(item){
        this.marked_case = !this.marked_case;
      if(this.marked_case === true){
        this.Pass_Quiz.push(item)
      }
      if(this.marked_case === false){
        console.log("Pass_Quiz false")
        this.Pass_Quiz =  this.Pass_Quiz.filter(e =>  e.id !== item.id)
      }
      },
      Previous(){
        this.Quiz_serial-- ;
        this.Compare();
      },
      Finish_Quiz(){
        console.log("Answered",this.Answered);
        console.log("Pass_Quiz",this.Pass_Quiz);
        localStorage.setItem(`Pass_Quiz_${this.$route.params.slug}`, JSON.stringify(this.Pass_Quiz));
        localStorage.setItem(`Answered_${this.$route.params.slug}`, JSON.stringify(this.Answered));
        localStorage.setItem(`Quiz_data_${this.$route.params.slug}`, JSON.stringify(this.Quiz_data));
        localStorage.setItem(`Quiz_duration${this.$route.params.slug}`, JSON.stringify((this.Minute*60)+this.Remseconds));
        this.$router.push({path:`/ResultOldStyle/${this.$route.params.slug}`})
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
.min_height{
  min-height: 250px;
}
.spinner_loading{
  height: 90vh;
}
.selected{
  border: 2px solid var(--BlueColor);
}
.Pagination_label{
  cursor: pointer;
}
.ImgManger{
  height: 100px;
  width: 500px;
}
@media (max-width:567px) {
  .ImgManger{
    width: 100%;
    height: 100%;
  }
}
.box{
  width: 20px;
  height: 20px;
}
.Responsive4{
  display: flex;
  flex-direction: column;
}
.Responsive{
  display: grid;
  grid-template-columns: auto  ;
}
.clock_img{
  width: 22px;
  margin-left: 2px;
}
.radioParent{
  width: fit-content;
}


</style>

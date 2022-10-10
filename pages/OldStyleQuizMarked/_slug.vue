<template >
<div>
  <AppNav/>
  <div >
  <div v-if="this.Quiz_data.length > 0 ">

    <b-row  align-h="center"  class="">
        <div class="mt-5">.</div>
        <div class="d-flex flex-wrap w-100 p-2 justify-content-between align-items-center bg-DarkBlueOldColor p-1">
          <b-col cols="11" sm="10"  md="8" lg="6" class="">
            <p class="m-0">اسم الاختبار- اسم المختبر</p>
          </b-col>
          <b-col cols="11" sm="10"  md="8" lg="6" class="d-flex flex-column align-items-end">
            <p class="m-0 f-12">
              <img :src="require(`~/assets/icon/clock.svg`)" alt="img" class="clock_img"/>
            الوقت المتبقي : {{Quiz_duration}}</p>
            <p class="m-0 f-12 mt-1">السؤال  <span class="">{{Quiz_serial+1}}</span> من <span class="">{{Quiz_data.length}}</span> سؤال</p>
          </b-col>
        </div>
    </b-row>

    <b-row class="flex-wrap align-items-center  justify-content-end  bg-BlueOldColor p-1">
      <!-- <p class="cursor text-white m-0 ml-5"  v-on:click="Pass"><img :src="require(`~/assets/icon/flag_top.svg`)" alt="img" class="clock_img"/> تميز السؤال للمراجعة </p> -->
      <b-dropdown id="dropdown-1" text="الخط" class="m-0 mr-5">
        <b-dropdown-item active>خط عادي</b-dropdown-item>
        <b-dropdown-item>خط عريض </b-dropdown-item>
        <b-dropdown-item>خط عريض بزياده</b-dropdown-item>
      </b-dropdown>
    </b-row>



      <b-row align-h="center"  class="px-3 align-items-start border sp_style">
        <b-col cols="11" sm="10"  md="8" lg="6" class="border_left pt-3">

          <b-row align-h="center"  class="flex-column flex-wrap justify-content-end pr-3">
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
                      v-on:click="Save(Quiz_data[Quiz_serial].id, option.value, Quiz_serial, false)"
                      class="radioParent"
                    >
                      <b-form-radio
                        name="some-radios"
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

        <b-col  cols="11" sm="10"  md="8" lg="6" class="text-center pt-3">
          <h5>أسئلة اختيار من متعدد</h5>
          <h6>فيما يلي سؤال يتبعه أربعة اختيارات</h6>
          <p>المطلوب اختيار الاجابة الصحيحية</p>

        </b-col>
      </b-row>

      <b-row  align-h="center"  class="flex-wrap-reverse  justify-content-between align-items-center bg-DarkBlueOldColor p-1">
        <b-col cols="12" sm="7" class="d-flex">
          <p class="m-0 border_right pl-3">المعادلات</p>
          <div class="mr-2 cursor f-18" v-on:click="Finish_Quiz"> الأنتقال لصفحة المراجعة</div>
        </b-col>
        <b-col cols="12" sm="5" class="d-flex justify-content-end">
          <div v-if="Quiz_serial > 0 "  v-on:click="Previous" class="cursor ml-2"><img :src="require(`~/assets/icon/arrow_right.svg`)" alt="img" class="clock_img ml-2"/>السابق</div>
          <div  v-if="Quiz_serial !== Quiz_data.length-1 " v-on:click="Next" class="cursor">التالي<img :src="require(`~/assets/icon/arrow_left.svg`)" alt="img" class="clock_img mr-2"/></div>
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

  export default {
    components:{
      Loading,
      AppNav
    },
    data() {
      return {
        Quiz_data: [],
        Answered:[],
        Marked_Answered:[],
        selected: '',
        status_code: '',
        Quiz_serial:0,
        Quiz_duration:0,
        Minute:0,
        Seconds:0,
        Remseconds:0,
        Delay_Qu : false,
      }
    },
    mounted() {
      this.CurrentState();

    },
    methods: {
      CurrentState(){
        this.Answered = JSON.parse(localStorage.getItem(`Answered_${this.$route.params.slug}`))
        this.Seconds = JSON.parse(localStorage.getItem(`Quiz_duration${this.$route.params.slug}`));
        JSON.parse(localStorage.getItem(`Answered_${this.$route.params.slug}`)).forEach(element => {
          if(element.Delay_Qu === true){
            this.Marked_Answered.push(element)
          }

        });
        JSON.parse(localStorage.getItem(`Quiz_data_${this.$route.params.slug}`)).forEach(element => {
          this.Marked_Answered.forEach(ele => {
            if(element.id === ele.id){
             this.Quiz_data.push(element)
            }
          });

        });
        console.log("Incompleted_Quiz_data",this.Quiz_data)
        console.log("Incompleted_Answered",this.Marked_Answered)
      },
      Compare(){
        if(this.Answered.length > 0){
          this.Answered.forEach(element => {
            if(element.my_Quiz_serial === this.Quiz_serial){
              this.selected = element.answer
            }
          });
        }

      },
      Save(id, option_value, my_Quiz_serial, Delay_Qu){
        if(this.Answered.length > 0){
          this.Answered.forEach(element => {
            if(element){
              if(element.id === id){
                element.answer = option_value;
                element.Delay_Qu = Delay_Qu;
              }
            }
          });
          // this.Answered.push({'id':id,'answer':option_value,'my_Quiz_serial':my_Quiz_serial, Delay_Qu:Delay_Qu});
        }

        console.log("this.Answered>>",this.Answered)

      },
      Next(){
        this.Quiz_serial++ ;
        this.Compare();
      },
      Pass(){
        this.Save(this.Quiz_data[this.Quiz_serial].id, '', this.Quiz_serial,true);
      },
      Previous(){
        this.Quiz_serial-- ;
        this.Compare();
      },
      Finish_Quiz(){
        localStorage.setItem(`Answered_${this.$route.params.slug}`, JSON.stringify(this.Answered));
        localStorage.setItem(`Quiz_duration${this.$route.params.slug}`, JSON.stringify((this.Minute*60)+this.Remseconds));
        this.$router.push({path:`/ResultOldStyle/${this.$route.params.slug}`})
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

<template>
  <div>
    <AppNav/>
    <div v-if="CurentCourse_data !== ''">
      <b-container>
        <b-row align-h="center"  class="flex-wrap">
          <b-col cols="12"  lg="7" class="m-sec">
            <div class="position-relative w-100">
              <img :src="require(`~/assets/icon/path.svg`)" class="path" alt="icon"/>
              <h3 class="text_blue">
                {{CurentCourse_data.name}}
              </h3>
            </div>

            <h6 class="text_yellow my-4">{{CurentCourse_data.price_rendered}}</h6>
            <p>فيديو شرح للدورة</p>

            <script src="https://vjs.zencdn.net/7.20.2/video.min.js"></script>

            <video
              id="my-video"
              class="video-js vjs-theme-sea video"
              controls
              preload="auto"
              data-setup='{
                "playbackRates": [0.25, 0.5, 1, 1.25,1.50, 1.75, 2]
              }'
            >

             <source :src="CurentCourse_data.video_introduction" type="video/mp4">

           </video>

          </b-col>
          <b-col cols="12"  lg="5" class="m-sec">

            <div class="d-flex flex-column justify-content-left align-items-end">

              <b-button  v-on:click="$router.push({path:`/Cources/${CurentCourse_data.id}`})" type="button" class="btn btn_Green rounded_0 px-5 py-2 mt-5 w-75"> شراء الدورة الان</b-button>
            </div>
            <p class="mt-5">:يتضمن البرنامج التدريبي</p>

            <div class="d-flex bgfillBlue border_blue_2 pr-3 pl-5 py-2 mt-4 ">
              <img :src="require(`~/assets/icon/Time Circle 1.svg`)" class="icon ml-3" alt="icon"/>
              <span>التوقيت  :</span>
              <span class="text_blue mr-2">{{CurentCourse_data.estimated_time}}</span>
            </div>

            <div class="d-flex bgfillGreen border_Green_2 pr-3 pl-5 py-2 mt-4">
              <img :src="require(`~/assets/icon/com.svg`)" class="icon ml-3" alt="icon"/>
              <span>المستوي:</span>
              <span class="text_green mr-2"> {{CurentCourse_data.level}}</span>
            </div>

            <div class="d-flex bgfillOrange border_orange_2 pr-3 pl-5 py-2 mt-4 ">
              <img :src="require(`~/assets/icon/des.svg`)" class="icon ml-3" alt="icon"/>
              <span>المحاضرات:</span>
              <span class="text_yellow mr-2">{{CurentCourse_data.lessons_estimated_number}} </span>
            </div>

            <div class="d-flex bgfillRed border_red_2 pr-3 pl-5 py-2 mt-4 ">
              <img :src="require(`~/assets/icon/icons Q2.svg`)" class="icon ml-3" alt="icon"/>
              <span class="text_red mr-2">تم تسجيل اكثر من 1000 طالب</span>
            </div>

            <div class="d-flex  mt-5 font-16">
              <img :src="require(`~/assets/img/Ellipse 970.png`)" class="person ml-3" alt="icon"/>
              <div>
                <p class="my-0 mt-1 text_Gray">المدرس</p>
                <p class="my-0 mt-1">الأستاذ: محمد المنصف</p>
              </div>
            </div>

          </b-col>

          <div class="my-4 text-right">
            <p class="font-16 ">لمحة عن الدورة</p>
            <div class="GrayLine bgGray">
              <div class="GreenLine bgGreen"></div>
            </div>
            <p class="text_GraySec mt-3" v-html="CurentCourse_data.content"></p>
          </div>


        </b-row>
      </b-container>
    </div>
    <div v-else class="d-flex justify-content-center align-items-center spinner_loading">
        <Loading/>
      </div>
  </div>

</template>

<script>
import config from "@/config";
import AppNav from "@/components/AppNav";
import Loading from "@/components/Loading";
export default {
  components:{
    AppNav,
    Loading,
  },
  data (){
    return {
      Course_data: [],
      CurentCourse_data: '',
    }
  },
  mounted() {
    this.fetchCurentCourses();
    this.CurentCourse();
  },
  methods: {
    fetchCurentCourses() {
      var myHeaders = new Headers();
      myHeaders.append("Authorization", `Bearer${config.token}`);

      var requestOptions = {
        method: 'GET',
        headers: myHeaders,
        redirect: 'follow'
      };

      fetch(config.apiUrl+"wp-json/learnpress/v1/courses", requestOptions)
        .then(response => response.text())
        .then(result => {
          this.Course_data = JSON.parse(result)
        })
        .catch(error => console.log('error', error));
    },
    CurentCourse(){
      setTimeout(() => {
        this.Course_data.forEach(element => {
          if(element.id.toString() === this.$route.params.slug ){
            this.CurentCourse_data = element
          }
        });
        console.log("this.CurentCourse_data",this.CurentCourse_data)
      }, 4000);
    },
  },

}
</script>


<style scoped>
  .spinner_loading{
  height: 90vh;
}
 .path{
    position: absolute;
    top: -20px;
    right: 280px;
    width: 40px;
  }
  .video{
    width: 100% ;
    height: 350px;
    border-radius: 20px !important;
  }

  .lock{
    width: 50px;
  }
  .GrayLine{
    width: 100%;
    height: 3px;
    position: relative;
  }
  .GreenLine{
    border-radius: 5px   5px 0 0;
    width: 10%;
    height: 9px;
    position:absolute ;
    top: -5px;
  }
  .person{
    width: 60px;
    height: 60px;
    border-radius: 50%;
  }
  .star{
    width: 20px;
    margin: 0 5px;
  }
  .justify-content-left{
    justify-content: left !important;
  }
</style>

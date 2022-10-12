<template>
  <div>
    <AppNav/>
    <div v-if="CurentCourse_data !== ''">
      <b-container>
        <b-row align-h="center"  class="flex-wrap-reverse">
          <b-col cols="12"  lg="5" class="text_GraySec m-sec">

            <div class="bgGray rounded_0 p-3 my-4" v-for="section in CurentCourse_data.sections" :key="section.id">
              <div class="d-flex justify-content-between" :id="section.id" v-on:click="Toggle(section.id)">
                <p> {{section.title}}</p>
                <img :src="require(`~/assets/icon/downUP.svg`)" class="downUP" alt="icon"/>
              </div>

              <div class="content" :id="section.id">

                <div v-for="item in section.items" :key="item.id">
                  <div v-on:click="CurentLessons(item.id)" :id="`id${item.id}`" class="d-flex justify-content-between align-items-center my-4 cursor_pointer list" v-if="item.type === 'lp_lesson'">
                    <div class="d-flex align-items-center" >
                      <img :src="require(`~/assets/img/play-button.png`)" class="iconCheck" alt="icon"/>
                      <p class="my-0 mr-2">{{item.title}}</p>
                    </div>
                    <p class="my-0">02:30</p>
                  </div>
                </div>

                <!-- <div class="d-flex justify-content-between align-items-center my-4">
                  <div class="d-flex align-items-center">
                    <img :src="require(`~/assets/icon/run.svg`)" class="iconCheck" alt="icon"/>
                    <p class="my-0 mr-2 text_green">نص وهمي لدرس الكورس</p>
                  </div>
                  <p class="my-0 text_green">02:30</p>
                </div>

                <div class="d-flex justify-content-between align-items-center my-4">
                  <div class="d-flex align-items-center">
                    <img :src="require(`~/assets/icon/puse.svg`)" class="iconCheck" alt="icon"/>
                    <p class="my-0 mr-2">نص وهمي لدرس الكورس</p>
                  </div>
                  <p class="my-0">02:30</p>
                </div> -->

              </div>

            </div>

          </b-col>
          <b-col cols="12"  lg="7" class="m-sec">
            <div v-if="CurentLessons_data !== ''">

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

              <source :src="CurentLessons_data.video_url" type="video/mp4">

            </video>

              <p class="my-3 font-16">{{CurentLessons_data.name}}<span class="text_yellow"> (متاحة للمشتركين بالدورة الشاملة مثلا)</span></p>

              <div v-if="CurentLessons_data.pdf_files !== null && CurentLessons_data.pdf_files[0]" class="shadow rounded_1 p-3 my-3 d-flex flex-wrap">
                <div class="bgfillBlue border-radius fileParent">
                  <img :src="require(`~/assets/icon/file22.svg`)" class="file" alt="icon"/>
                </div>
                <div class="mr-3">
                  <p class="my-0">ملف {{CurentLessons_data.pdf_files[0].file_name}}</p>
                  <p class="text_green mt-1">
                    <span class="ml-1">بحجم</span>
                    {{Math.ceil(CurentLessons_data.pdf_files[0].pdf_file.filesize/1000000)}}
                    <sapn class="mr-1">ميجا</sapn>
                  </p>
                </div>
                <div class="mr-auto">
                  <a  :href="CurentLessons_data.pdf_files[0].pdf_file.url" target="_blank">
                    <img :src="require(`~/assets/icon/pdf.svg`)" class="pdf ml-5" alt="icon"/>
                  </a>
                  <b-button v-on:click="DownLoad(CurentLessons_data.pdf_files[0].pdf_file)" size="sm" class="btn btn_blue my-2 py-2 px-5 rounded_0" type="button" > تحميل</b-button>
                </div>
              </div>


              <div v-if="CurentLessons_data.pdf_files !== null && CurentLessons_data.pdf_files[1]" class="shadow rounded_1 p-3 my-3 d-flex flex-wrap">
                <div class="bgfillBlue border-radius fileParent">
                  <img :src="require(`~/assets/icon/file22.svg`)" class="file" alt="icon"/>
                </div>
                <div class="mr-3">
                  <p class="my-0">ملف {{CurentLessons_data.pdf_files[1].file_name}}</p>
                  <p class="text_green mt-1">
                    <span class="ml-1">بحجم</span>
                    {{Math.ceil(CurentLessons_data.pdf_files[1].pdf_file.filesize/1000000)}}
                    <sapn class="mr-1">ميجا</sapn>
                  </p>
                </div>
                <div class="mr-auto">
                  <a  :href="CurentLessons_data.pdf_files[1].pdf_file.url" target="_blank">
                    <img :src="require(`~/assets/icon/pdf.svg`)" class="pdf ml-5" alt="icon"/>
                  </a>
                  <b-button v-on:click="DownLoad(CurentLessons_data.pdf_files[1].pdf_file)" size="sm" class="btn btn_blue my-2 py-2 px-5 rounded_0" type="button" > تحميل</b-button>
                </div>
              </div>

              <div  v-if="CurentLessons_data.pdf_files !== null" class="orangeLind"></div>


              <div v-if="Number.isInteger(CurentLessons_data.quiz_id) === true" class="shadow rounded_1 p-3 my-3 d-flex flex-wrap">
                <div class="bgfillBlue border-radius fileParent">
                  <img :src="require(`~/assets/icon/testfile.svg`)" class="file" alt="icon"/>
                </div>
                <div class="mr-3">
                  <p class="my-0"> اختبار الكتروني</p>
                  <p class="text_green mt-1">عدد ..... سؤال</p>
                </div>
                <div class="mr-auto">
                  <b-button v-b-modal.modal-Quiz v-on:click = "ChangePath(CurentLessons_data.quiz_id)" size="sm" class="btn btn_Green my-2 py-2 px-5 rounded_0" type="button" > ابدا الان</b-button>
                </div>
              </div>

              <b-modal id="modal-Quiz" title="اختر نظام الاختبار" hide-footer>
                <div class="d-flex flex-wrap justify-content-center">
                  <div v-on:click = "ChosseNewPath()" class="bgGreen rounded block m-2">
                    <p class="my-4 text-white font-16">الأختبار</p>
                    <img :src="require(`~/assets/icon/lateww.svg`)" alt="img" class="clock_img"/>
                  </div>

                  <div v-on:click = "ChosseOldPath()" class="bluebg  rounded block m-2">
                    <p class="my-4 text-white font-16">اختبار بنظام محاكي</p>
                    <img :src="require(`~/assets/icon/lateww.svg`)" alt="img" class="clock_img"/>
                  </div>
                </div>

              </b-modal>

              <div v-if="CurentLessons_data.pdf_files !== null && CurentLessons_data.pdf_files[2]" class="orangeLind"></div>


              <div v-if="CurentLessons_data.pdf_files !== null && CurentLessons_data.pdf_files[2]" class="shadow rounded_1 p-3 my-3 d-flex flex-wrap">
                <div class="bgfillOrange border-radius fileParent">
                  <img :src="require(`~/assets/icon/fillornge222.svg`)" class="file" alt="icon"/>
                </div>
                <div class="mr-3">
                  <p class="my-0">ملف {{CurentLessons_data.pdf_files[2].file_name}}</p>
                  <p class="text_blue mt-1">
                    <span class="ml-1">بحجم</span>
                    {{Math.ceil(CurentLessons_data.pdf_files[2].pdf_file.filesize/1000000)}}
                    <sapn class="mr-1">ميجا</sapn>
                  </p>
                </div>
                <div class="mr-auto">
                  <a  :href="CurentLessons_data.pdf_files[2].pdf_file.url" target="_blank">
                    <img :src="require(`~/assets/icon/pdf.svg`)" class="pdf ml-5" alt="icon"/>
                  </a>
                  <b-button v-on:click="DownLoad(CurentLessons_data.pdf_files[2].pdf_file)" size="sm" class="btn btn_blue my-2 py-2 px-5 rounded_0" type="button" > تحميل</b-button>
                </div>
              </div>

              <div v-if="CurentCourse_data.secondary_courses.length > 0">
                <h5 class="mt-5 text_dark">دورات مجانية</h5>
                <b-row align-h="center"  class="flex-wrap align-items-center">
                  <b-col
                   cols="10" sm="10" md="8"  lg="6" class="mb-4 py-2 px-4 cursor_pointer"
                   v-for="item in CurentCourse_data.secondary_courses" :key="item.id"
                   v-on:click="$router.push({path:`/Session/${item.id}`})"

                  >
                    <div class="parent">
                      <img :src="require(`~/assets/img/scott0.png`)" class="w-100 rounded" alt="icon"/>
                      <div class="overly rounded">
                        <div class="d-flex bgGreen my-2 mx-2 p-2 rounded_0" >
                          <img :src="require(`~/assets/icon/share.svg`)" class="icon" alt="icon"/>
                        </div>
                      </div>
                    </div>
                    <h5 class="text_blue mt-2 font-weight-bold my-3" v-html="item.title"></h5>
                    <div class="d-flex align-items-center my-3">
                      <img :src="require(`~/assets/icon/price-tag.svg`)" class="icon" alt="icon"/>
                      <p class="mr-2 my-0">مجانية</p>
                    </div>
                  </b-col>
                </b-row>
              </div>

            </div>
            <div v-else>
              <h5 class="font-weight-bold text-center mt-5"> لا يوجد محتوي </h5>
            </div>

          </b-col>
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
    data() {
      return {
        CurentCourse_data: '',
        Lessons_data: [],
        CurentLessons_data: '',
        path_id : '',
      }
    },
    mounted() {
    this.fetchCurentCourses();
    this.fetchCurentLessons();

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
            this.CurentCourse(JSON.parse(result));
          })
          .catch(error => console.log('error', error));
      },
      fetchCurentLessons() {
        var myHeaders = new Headers();
        myHeaders.append("Authorization", `Bearer${config.token}`);

        var requestOptions = {
          method: 'GET',
          headers: myHeaders,
          redirect: 'follow'
        };

        fetch(config.apiUrl+"wp-json/learnpress/v1/lessons", requestOptions)
          .then(response => response.text())
          .then(result => {
            this.Lessons_data = JSON.parse(result)
            console.log("JSON.parse(result)",JSON.parse(result))
          })
          .catch(error => console.log('error', error));
      },
      CurentCourse(Course_data){
        Course_data.forEach(element => {
          if(element.id.toString() === this.$route.params.slug ){
            this.CurentCourse_data = element
          }
        });

        setTimeout(() => {
          this.CurentCourse_data.sections[0].items.forEach(element => {
            if(element.type === 'lp_lesson'){
              this.CurentLessons(element.id);
              document.querySelector(`#id${element.id}`).classList.add('activeList');
            }
          });

        }, 500);

      },
      CurentLessons(item_id){

        this.Lessons_data.forEach(element => {
          if(element.id === item_id ){
            this.CurentLessons_data = element
          }
        });

        document.querySelectorAll('.list').forEach(ele =>{
          ele.classList.remove('activeList')
        })
        document.querySelector(`#id${item_id}`).classList.add('activeList')
        console.log("this.CurentLessons_data",this.CurentLessons_data)

      },
      Toggle(id){
        document.querySelectorAll('.content').forEach(ele =>{
          if(ele.id === id.toString()){
            ele.classList.toggle('d-none')
          }
        });

      },
      DownLoad(pdf_file){
        var FileSaver = require('file-saver');

        var blob = new Blob(["Hello, world!"], {type: "text/plain;charset=utf-8"});

        // FileSaver.saveAs(blob, "hello world.txt");
        var oReq = new XMLHttpRequest();
        // The Endpoint of your server
        var URLToPDF = pdf_file.url;

        // Configure XMLHttpRequest
        oReq.open("GET", URLToPDF, true);

        // Important to use the blob response type
        oReq.responseType = "blob";

        // When the file request finishes
        // Is up to you, the configuration for error events etc.
        oReq.onload = function() {
            // Once the file is downloaded, open a new window with the PDF
            // Remember to allow the POP-UPS in your browser
            var file = new Blob([oReq.response], {
              type: 'application/pdf'
            });

            // Generate file download directly in the browser !
            saveAs(file, pdf_file.filename);
        };

        oReq.send();

        setTimeout(() => {
          if(oReq.status === 0){
            alert("You must give permission to download from the browser settings")
          }
        }, 2000);
        console.log("oReq",oReq)
      },
      ChangePath(id){
        this.path_id = id;
        if(screen.width <= 992){
          this.$router.push({path:`/Quiz/${id}`})
        }
      },
      ChosseNewPath(){
        this.$router.push({path:`/Quiz/${this.path_id}`})
      },
      ChosseOldPath(){
        this.$router.push({path:`/OldStyleQuiz/${this.path_id}`})
      },
    },

  };

  </script>


<style scoped>
  .spinner_loading{
  height: 90vh;
}

  .video {
    width: 100% ;
    height: 400px;
  }
  .lock{
    width: 50px;
  }
  .file,.iconCheck{
    width: 30px;
  }
  .pdf{
    width: 30px;
    cursor: pointer;
  }
  .downUP{
    cursor: pointer;
  }
  .fileParent{
    width: 60px;
    height: 60px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .orangeLind{
    width:150px;
    height: 3px;
    background-color: var(--YellowColor);
    margin: 30px auto;
  }
  .parent{
  position: relative;
}
.overly{
  position: absolute;
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
  background-image: url('~/assets/img/Rectangle 45.png');
  width: 100%;
  display: flex;
  justify-content: end;
  align-items: flex-start;
}
.activeList{
  color: #039A7B;
}
.clock_img{
  width: 25px;
  margin: auto;
}
.block{
  width: 170px;
  height: 140px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}
</style>

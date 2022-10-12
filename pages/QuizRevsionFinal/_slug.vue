<template >
<div>
  <AppNav/>
  <div class="" >
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


          <div id="list1" class="dropdown-check-list visible cursor_pointer bgfillGreen border_Green_2 px-3 py-2 mt-5 font-16" tabindex="100">
            <span class="anchor ">
              <img :src="require(`~/assets/icon/file0.svg`)" class="icon ml-2" alt="icon"/>
              <span class="text_green"> اضف السؤال لمجلد</span>
            </span>
            <ul class="items FoldersListCheckbox mt-2"  v-for="list in FoldersList" :key="list.index">
              <div class="d-flex justify-content-between">
                <li class="d-flex" v-on:click="FoldersListCheckbox(Quiz_data[Quiz_serial])">
                    <input type="checkbox" :class="list.title" :id="list.title"/>
                    <label :for="list.title" class="mx-2">{{list.title}}</label>
                  </li>

                <div>
                  <span
                    class="cursor_pointer text-danger font-weight-bold"
                    v-on:click="RemaoveFolderListCheckbox(list)"
                  >x
                  </span>
                  <span
                    class="cursor_pointer font-weight-bold"
                    v-on:click="EditFolderListCheckboxItem = list; EditeListName = list.title"
                    v-b-modal.modal-EditList
                  >
                  <img :src="require(`~/assets/icon/edit.png`)" class="icon mr-2" alt="icon"/>
                  </span>
                </div>
              </div>

            </ul>
          </div>

          <b-modal id="modal-EditList" title="تعديل اسم المجلد" hide-footer>
            <b-form-input v-model="EditeListName" class="my-4" placeholder="اكتب اسم المجلد"></b-form-input>
            <b-button size="sm" class="btn btn_Green my-2 py-2 px-r px-l rounded_0" type="button"  v-on:click="EditFolderListCheckbox(EditFolderListCheckboxItem)"> تعديل</b-button>
          </b-modal>

          <img
            :src="require(`~/assets/icon/plus.png`)"
            class="icon mr-3 cursor_pointer"
            alt="icon"
            v-b-modal.modal-addList
          />

          <b-modal id="modal-addList" title="إضافة مجلد جديد" hide-footer>
            <b-form-input v-model="ListName" class="my-4" placeholder="اكتب اسم المجلد"></b-form-input>
            <b-button size="sm" class="btn btn_Green my-2 py-2 px-r px-l rounded_0" type="button"  v-on:click="CreateList"> إنشاء</b-button>
          </b-modal>


          <div class="my-5 d-flex justify-content-between">
            <b-button size="sm" class="btn btn_red my-2 py-2 px-r px-l rounded_0" type="button" v-if="Quiz_serial > 0 " v-on:click="Previous"> السابق</b-button>
            <b-button size="sm" class="btn btn_yellow my-2 py-2 px-r px-l rounded_0 " type="button" v-if="Quiz_serial !== Quiz_data.length-1 " v-on:click="Next"> التالي</b-button>
            <b-button size="sm" class="btn btn_yellow my-2 py-2 px-r px-l rounded_0 " type="button" v-if="Quiz_serial === Quiz_data.length-1 " v-on:click="Finish_Quiz"> المراجعة</b-button>
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

  export default {
    components:{
      Loading,
      AppNav
    },
    data() {
      return {
        Quiz_data: [],
        Answered_obj : {},
        Answered:[],
        Favorite_Quiz:[],
        Pass_Quiz:[],
        selected: '',
        status_code: '',
        Quiz_serial:0,
        HeartCase: false,
        Favorite_Quiz :[],
        PassCase:false,
        Pass_Quiz :[],
        ListName: '',
        EditeListName:'',
        FoldersList:[{title: 'default', content: []}],
        EditFolderListCheckboxItem: '',
        Result :[],
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
        this.Answered = JSON.parse(localStorage.getItem(`Answered_${this.$route.params.slug}`));
        this.Quiz_data = JSON.parse(localStorage.getItem(`Quiz_data_${this.$route.params.slug}`));
        this.Result = JSON.parse(localStorage.getItem(`Result_${this.$route.params.slug}`));
        if(JSON.parse(localStorage.getItem(`Quiz_serial${this.$route.params.slug}`)) !== null){
          this.Quiz_serial = JSON.parse(localStorage.getItem(`Quiz_serial${this.$route.params.slug}`))
        }
        console.log("localStorage_Answered",this.Answered)
      },
      Compare(){
        setTimeout(() => {
          if(this.Answered.length > 0){
          this.Answered.forEach(element => {
            if(element.my_Quiz_serial === this.Quiz_serial){
              if(this.Result.results.answered[element.id].correct === true){
                document.querySelector(`.class${element.answer}`).classList.add('selected')
              }
              if(this.Result.results.answered[element.id].correct === false){
                this.Result.results.answered[element.id].options.forEach(ele => {
                  if(ele.is_true === 'yes'){
                    document.querySelector(`.class${ele.value}`).classList.add('selected')
                  }
                });
                document.querySelector(`.class${this.Result.results.answered[element.id].answered.answered}`).classList.add('Wrongselected')

              }
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
      localStorage.setItem(`Answered_${this.$route.params.slug}`, JSON.stringify(this.Answered));
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
    Drop(){
      document.querySelector('.anchor').addEventListener('click',()=>{
        document.getElementById('list1').classList.toggle('visible');
      })
    },
    CreateList(){
      if(this.ListName !== ''){
        this.FoldersList.push({title:this.ListName, content:[]})
      }
      this.ListName = '';
      console.log('this.FoldersList',this.FoldersList)
    },
    FoldersListCheckbox(item){

      this.FoldersList.forEach(ele => {
        ele.content = ele.content.filter(e => e !== item)
      });

      document.querySelectorAll('.FoldersListCheckbox input').forEach(element => {
        if(element.checked){
          console.log("FoldersListCheckbox", element.className)
          this.FoldersList.forEach(ele => {
            if(ele.title === element.className){
              ele.content.push(item)
            }
          });
        }
      });
      console.log("this.FoldersList", this.FoldersList)
    },
    RemaoveFolderListCheckbox(item){
      this.FoldersList = this.FoldersList.filter(e => e !== item)
    },
    EditFolderListCheckbox(item){
      console.log("EditFolderListCheckbox",item)
      this.FoldersList.forEach(ele => {
        if(ele.title === item.title){
          item.title = this.EditeListName;
        }
      });
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
 .selected{
  outline: 2px solid rgb(15, 192, 124);
  outline-offset: 5px;
 }


/* DropList */
.dropdown-check-list {
  display: inline-block;
}

.dropdown-check-list .anchor {
  position: relative;
  cursor: pointer;
  display: inline-block;
}

.dropdown-check-list .anchor:after {
  position: absolute;
  content: "";
  border-left: 2px solid #039A7B;
  border-top: 2px solid #039A7B;
  padding: 5px;
  right: 270px;
  top: 20%;
  transform: rotate(-135deg);
}

.dropdown-check-list .anchor:active:after {
  right: 270px;
  top: 21%;
}

.dropdown-check-list ul.items {
  padding: 2px;
  display: none;
  margin: 0;
  border-top: none;
}

.dropdown-check-list ul.items li {
  list-style: none;
  display: flex !important;

}

.dropdown-check-list.visible .anchor {
  color: #0094ff;
}

.dropdown-check-list.visible .items {
  display: block;
}

.Wrongselected{
  outline: 2px solid rgb(221, 15, 15);
  outline-offset: 5px;
 }


</style>

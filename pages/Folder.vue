<template>
  <div>
    <div v-if="this.FoldersList.length > 0">
        <AppNav/>
      <b-container class="" >
        <div class="mb-sec">.</div>
        <div class="d-flex flex-wrap justify-content-between align-items-center">
          <p class="font-16 my-0">اسم الحافظة التي تم الدخول لها</p>
          <div class="d-flex flex-wrap align-items-center">
            <b-button size="sm"  class="btn bg_liner  my-2 py-3 px-4  rounded " type="button"  v-on:click="Show"> اختر</b-button>
            <b-button size="sm"  class="btn bg_liner  my-2 py-3 px-4 mr-5 rounded " type="button" v-if="CurrentList.questions.length > 0" v-on:click="StartQuiz(item)">ابدء الاختبار</b-button>
            <select id="FoldersList"  class="FoldersListInput">
              <option value="none" selected disabled hidden>اسم الحافظة </option>
              <option v-for="list in FoldersList" :key="list.index" :value="list.name" >{{list.name}}</option>
            </select>
          </div>

        </div>
        <div v-if="CurrentList.questions.length > 0">
          <div  v-for="item in CurrentList.questions" :key="item.index" class="FoldersListItem my-3">
            <img :src="item.thumbnail"  alt="img" class="thumbnail"/>
            <img :src="require(`~/assets/icon/remove.svg`)" v-on:click="Remove(item)" alt="img" class="remove"/>
          </div>
        </div>

        <div v-if="CurrentList.questions.length === 0">
          <h5 class="text-center mt-5"> الحافظة فارغة</h5>
        </div>

      </b-container>
    </div>
    <div v-else class="d-flex justify-content-center align-items-center spinner_loading">
        <Loading/>
    </div>
  </div>
</template>

<script>
import AppNav from '@/components/AppNav';
import Loading from "@/components/Loading";
import config from "@/config";

export default {
  components:{
    Loading,
    AppNav,
  },
  data (){
    return {
      FoldersList:[{name:''}],
      id:'',
      CurrentList:{questions:[]},
    }
  },
  mounted(){
    setTimeout(() => {
      this.FetchFolders();
    }, 500);
  },
  methods:{
    FetchFolders(){
      var myHeaders = new Headers();
      myHeaders.append("Authorization", `Bearer${config.token}`);
      myHeaders.append("Cookie", "__wpdm_client=f5ddc77fd332e35ab25f445937d36c7c");

      var requestOptions = {
        method: 'GET',
        headers: myHeaders,
        redirect: 'follow'
      };

      fetch(config.apiUrl+"wp-json/learnpress/v1/folders", requestOptions)
        .then(response => response.text())
        .then(result => {
          this.FoldersList = JSON.parse(result);
          console.log('item  FoldersList', JSON.parse(result))
          console.log('item  FoldersList', this.FoldersList)


        })
        .catch(error => console.log('error', error));
    },
    Show(){
      this.FoldersList.forEach(element => {
        if(element.name === document.querySelector('#FoldersList').value){
          this.id = element.id ;
        }
      });
      var myHeaders = new Headers();
      myHeaders.append("Authorization", `Bearer${config.token}`);
      myHeaders.append("Cookie", "__wpdm_client=f5ddc77fd332e35ab25f445937d36c7c");

      var requestOptions = {
        method: 'GET',
        headers: myHeaders,
        redirect: 'follow'
      };

      fetch(config.apiUrl+`wp-json/learnpress/v1/folders/${this.id}`, requestOptions)
        .then(response => response.text())
        .then(result => {
          this.CurrentList = JSON.parse(result);
          console.log("this.CurrentList",this.CurrentList)
        })
        .catch(error => console.log('error', error));
    },
    Remove(item){
      var myHeaders = new Headers();
      myHeaders.append("Authorization", `Bearer${config.token}`);
      myHeaders.append("Content-Type", "application/json");
      myHeaders.append("Cookie", "__wpdm_client=f5ddc77fd332e35ab25f445937d36c7c; _learn_press_session_079eddece82f2d2937cd2c203a8195b0=77e4246fa580e1b1de925170f59b9887%7C%7C1665855786%7C%7Ca35f3656287cbaac2c9668ecdd670d92");

      var raw = JSON.stringify({
        "folder_id": parseInt(this.id),
        "question_id": item.id
      });

      var requestOptions = {
        method: 'DELETE',
        headers: myHeaders,
        body: raw,
        redirect: 'follow'
      };

      fetch(config.apiUrl+"wp-json/learnpress/v1/folders/question", requestOptions)
        .then(response => response.text())
        .then(result =>{
          this.Show();
        })
        .catch(error => console.log('error', error));
    },
    StartQuiz(){
      this.$router.push({path:`/FoldersQuiz/${this.id}`})
    },
  },
}
</script>

<style scoped>
.spinner_loading{
  height: 90vh;
}
.FoldersListInput{
  background-color: #F3F3F3;
  color:#73758B;
  border: none;
  width: 280px;
  height: 45px;
  padding: 5px 9px;
  border-radius: 10px;
  margin-right: 20px;
  cursor: pointer;
}
.FoldersListInput:focus{
  border: #73758B 1px solid;
  outline: none;
}
.FoldersListInput option{
  background-color: #F3F3F3;
  border: none;
}
.FoldersListItem{
  background-color: #F3F3F3;
  padding: 15px;
  border-radius: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
}
.thumbnail{
  width: 50%;
  height: 90px;
}
.remove{
  cursor: pointer;
  width: 40px;
}
</style>

<template>
  <div>
    <div v-if="this.FoldersList.length > 0">
        <AppNav/>
      <b-container class="" >
        <div class="mb-sec">.</div>
        <div class="d-flex flex-wrap justify-content-between align-items-center">
          <p class="font-16 my-0">اسم الحافظة التي تم الدخول لها</p>
          <div class="d-flex flex-wrap align-items-center">
            <b-button size="sm"  class="btn bg_liner  my-2 py-3 px-4  rounded " type="button"  v-on:click="Show">ابدء الاختبار</b-button>
            <select id="FoldersList"  class="FoldersListInput">
              <option value="none" selected disabled hidden>اسم الحافظة </option>
              <option v-for="list in FoldersList" :key="list.index" :value="list.title" >{{list.title}}</option>
            </select>
          </div>

        </div>

        <div v-for="item in CurrentList" :key="item.index" class="FoldersListItem my-3">
          <img :src="item.thumbnail" alt="img" class="thumbnail"/>
          <img :src="require(`~/assets/icon/remove.svg`)" v-on:click="Remove(item)" alt="img" class="remove"/>
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

export default {
  components:{
    Loading,
    AppNav,
  },
  data (){
    return {
      FoldersList:[],
      CurrentList:[],
    }
  },
  mounted(){
    this.FoldersList = JSON.parse(localStorage.getItem(`FoldersList}`));
    console.log("FoldersList",this.FoldersList)
  },
  methods:{
    Show(){
      this.FoldersList.forEach(element => {
        if(element.title === document.querySelector('#FoldersList').value){
          this.CurrentList = element.content ;
        }
      });
    },
    Remove(item){
      this.CurrentList = this.CurrentList.filter(e => e !== item)
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

<template>
  <div>
    <AppNav/>
    <b-container class="my-4" >
      <div v-if="this.Namadhij.length > 0 ">
      <h3 class="OrangeColor text-center ">نماذج إلكترونية</h3>

      <div class="d-flex justify-content-between align-items-center my-3">
        <p class="BlueColor">{{Namadhij[$route.params.slug].title.rendered}}</p>
        <p class="DarkBlueSecColor">عدد النماذج : {{Namadhij[$route.params.slug].acf.quizzes_folder.length}}</p>
      </div>

        <b-row align-h="center"  class="justify-content-center align-items-center">
          <b-col v-for=" item in Namadhij[$route.params.slug].acf.quizzes_folder" :key="item.id"  cols="11" sm="10"  md="5" lg="4" class="mx-auto my-3">
            <div class="bg_item" v-on:click = "ChangePath(item.id)">
              <div class="overly">
                <div class="data">
                  <h5 class="text-center text-white mt-1 mb-3">{{item.title}}</h5>
                </div>
              </div>
            </div>
          </b-col>
        </b-row>


      </div>

      <div v-else class="d-flex justify-content-center align-items-center spinner_loading">
          <Loading/>
      </div>
    </b-container>
  </div>
</template>

<script>
import Loading from "@/components/Loading";
import AppNav from '@/components/AppNav';
  export default {
    components:{
      AppNav,
      Loading,
    },
    data() {
      return {
        Mode: false,
        Namadhij:[],
        item_id: '',
      }
    },
    mounted() {
      this.Namadhij = JSON.parse(localStorage.getItem("Namadhij"));
    },
    methods: {

      ChangePath(id){
        this.item_id = id;
          this.$router.push({path:`/Quiz/${id}`})
      },

    },


  }
</script>

<style scoped>
.bg_item{
  background-image: url('~/assets/img/item.png');
  border-radius:10px;
  width: 100%;
  height: 200px;
  cursor: pointer;
}
.overly{
  background-image: url('~/assets/img/overly.png');
  width: 100%;
  height: 100%;
  border-radius:10px;
  padding: 6px;
}
.data{
  border: 1px solid #fff;
  border-radius:10px;
  width: 100%;
  height: 100%;
}
.clock_img{
  width: 35px;
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

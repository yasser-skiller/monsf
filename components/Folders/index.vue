<template>
  <b-container>
      <div v-if="this.folders.length > 0 " >

        <div class="mb-sec">.</div>
        <h3 class="OrangeColor text-center">المجلدات</h3>



        <b-row align-h="center"  class="justify-content-center align-items-center">
          <b-col v-for=" (folder,index) in folders" :key="folder.id" cols="11" sm="10"  md="5" lg="4" class="mx-auto my-3">
            <div class="bg_item" v-on:click = "$router.push({path:`/FoldersDetails/${index}`})">
              <div class="overly">
                <div class="data">
                  <h5 class="text-center text-white mt-1 mb-3">{{folder.title.rendered}}</h5>
                  <ul v-for="quizze in folders[index].acf.quizzes_folder" :key="quizze.id">
                    <li class="text-white f-14 mb-2">{{quizze.title}}</li>
                  </ul>
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
</template>

<script>
import config from "@/config";
import Loading from "@/components/Loading";

  export default {
    components:{
      Loading
    },
    data() {
      return {
        folders:[],
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

        // var raw = JSON.stringify({"id":"95"});

        var requestOptions = {
          method: 'GET',
          headers: myHeaders,
          // body: raw,
          redirect: 'follow'
        };

        fetch(config.apiUrl+"wp-json/wp/v2/folder-quizzes?_fields=title,id,acf", requestOptions)
        .then(response => response.text())
        .then(res => {
          this.folders = JSON.parse(res);
          localStorage.setItem("Namadhij", JSON.stringify(JSON.parse(res)));
        })
        .catch (error => console.log(error));
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
  overflow-y: auto;
}
::-webkit-scrollbar {
  width: 5px;
}

::-webkit-scrollbar-track {
  -webkit-box-shadow: inset 0 0 6px rgba(200,200,200,1);
  border-radius: 10px;
}

::-webkit-scrollbar-thumb {
  border-radius: 10px;
  background-color:#fff;
  -webkit-box-shadow: inset 0 0 6px rgba(90, 90, 90, 0.7);
}
</style>

<template>
    <b-container class="m-sec" id="Coures">
      <h5 class="font-weight-bold animate__animated animate__fadeInRight">كورسات المنصف</h5>
      <div v-if="this.PublishedCourses_data.length > 0 ">
        <b-row align-h="center"  class="flex-wrap align-items-center">
          <b-col
           cols="10" sm="10" md="8"  lg="6" class="mb-4 py-2 px-4 cursor_pointer"
           v-for="item in PublishedCourses_data" :key="item.id"
           v-on:click="$router.push({path:`/Session/${item.id}`})"
          >
            <div class="parent">
              <img :src="item.image" class="w-100 rounded" alt="icon"/>
              <div class="overly rounded">
                <div class="d-flex bgGreen my-2 mx-2 p-2 rounded_0" >
                  <img :src="require(`~/assets/icon/share.svg`)" class="icon" alt="icon"/>
                </div>
              </div>
            </div>
            <h5 class="text_blue mt-2 font-weight-bold my-3" v-html="item.name"></h5>
            <div class="d-flex align-items-center ">
              <img :src="require(`~/assets/icon/book.svg`)" class="icon" alt="icon"/>
              <p class="mr-2 my-0">تحتوي علي <span>{{item.lessons_estimated_number}}</span></p>
            </div>
            <div class="d-flex align-items-center my-3">
              <img :src="require(`~/assets/icon/price-tag.svg`)" class="icon" alt="icon"/>
              <p class="mr-2 my-0">{{item.price_rendered}}</p>
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
    Loading,
  },
  data (){
    return {
      PublishedCourses_data: [],
    }
  },
  mounted() {
    this.fetchCourses();

  },
  methods: {
    fetchCourses() {
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
          this.PublishedCourses_data_method(JSON.parse(result));
        })
        .catch(error => console.log('error', error));
    },
    PublishedCourses_data_method(Courses_data){
      setTimeout(() => {
        Courses_data.forEach(element => {
          if(element.show_in_homepage === true ){
            if(element.status === 'publish'){
              this.PublishedCourses_data.push(element)
            }
          }
        });
      }, 4000);

    },
  },

};

</script>

<style scoped>
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
.icon{
  width: 15px;
}
</style>

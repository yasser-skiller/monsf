<template>
  <div>
    <AppNav/>
    <b-container class="" >
      <div v-if="this.Result.status === 'success'  ">
        <div class="mb-sec">.</div>
        <b-row  align-h="center"  class="flex-wrap  justify-content-between align-items-center p-1">
          <b-col cols="11" sm="10"  md="8" lg="6" class="">
            <img v-if="(Result.results.user_mark/Result.results.mark)*100 >= 50" :src="require(`~/assets/icon/testResult.svg`)" class="" alt="icon"/>
            <img v-if="(Result.results.user_mark/Result.results.mark)*100 < 50" :src="require(`~/assets/img/Group 35205.png`)"  class="w-100" alt="icon"/>
            <h5 class="text-center my-4">تقرير نتيجة الامتحان الخاص بك</h5>

            <div
             :class="`${(Result.results.user_mark/Result.results.mark)*100 > 50  ? 'bg_liner' : 'bg_linerFail'} rounded text-center text-white py-2 px-5 fit_width mx-auto` "
            >
              <h5 class="my-2"  v-if="(Result.results.user_mark/Result.results.mark)*100 > 50">ناجح</h5>
              <h5 class="my-2" v-else>راسب</h5>
              <small class=" my-1">بنسبة</small>
              <h5 class="font-weight-bold">{{(Result.results.user_mark/Result.results.mark)*100}}%</h5>
            </div>

          </b-col>
          <b-col cols="11" sm="10"  md="8" lg="6" class="">
            <div class="rounded_1 my-4 font-16 px-4 py-3 bg_gray d-flex justify-content-between align-items-center">
              <p class="text_blue my-0">درجة الامتحان</p>
              <p v-if="(Result.results.user_mark/Result.results.mark)*100 > 50" class="bgfillGreen text_green my-0 p-2 px-4 rounded">{{(Result.results.user_mark/Result.results.mark)*100}}%</p>
              <p class="bgfillRed text_red my-0 p-2 px-4 rounded">{{(Result.results.user_mark/Result.results.mark)*100}}%</p>
            </div>
            <div class="rounded_1 my-4 font-16 px-4 py-3 bg_gray d-flex justify-content-between align-items-center">
              <p class="text_blue my-0"> الحالة</p>
              <p v-if="(Result.results.user_mark/Result.results.mark)*100 > 50" class="bgfillGreen text_green my-0 p-2 px-4 rounded">ناجح</p>
              <p class="bgfillRed text_red my-0 p-2 px-4 rounded">راسب</p>
            </div>
            <div class="rounded_1 my-4 font-16 px-4 py-3 bg_gray d-flex justify-content-between align-items-center">
              <p class="text_blue my-0"> عدد الأسئلة التي تم اجابتها</p>
              <p class="bg_BBB text_blue my-0 p-2 px-4 rounded">{{Result.results.question_answered}}</p>
            </div>
            <div class="rounded_1 my-4 font-16 px-4 py-3 bg_gray d-flex justify-content-between align-items-center">
              <p class="text_blue my-0">عدد الأسئلة الصحيحة </p>
              <p class="bgfillGreen text_green my-0 p-2 px-4 rounded">{{Result.results.question_correct}}</p>
            </div>
            <div class="rounded_1 my-4 font-16 px-4 py-3 bg_gray d-flex justify-content-between align-items-center">
              <p class="text_blue my-0"> عدد الأسئلة الخاطئة</p>
              <p class="bgfillRed text_red my-0 p-2 px-4 rounded">{{Result.results.question_wrong}}</p>
            </div>
            <div class="rounded_1 my-4 font-16 px-4 py-3 bg_gray d-flex justify-content-between align-items-center">
              <p class="text_blue my-0"> عدد الأسئلة غير محلولة</p>
              <p class="bgfillGreen text_red my-0 p-2 px-4 rounded">{{Result.results.question_empty}}</p>
            </div>
          </b-col>

          <b-button
           v-if="old !== 'old'"
           v-on:click="$router.push({path:`/ResultsRevsion/${$route.params.slug}`})"
           size="sm"
           class="btn btn_blue my-2 py-3 px-5 rounded_0 mx-auto"
           type="button"
          > مراجعة
          </b-button>


        </b-row>
      </div>
      <div v-else class="d-flex justify-content-center align-items-center spinner_loading">
        <Loading/>
      </div>
    </b-container>
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
    data() {
      return {
        Result:[],
        Minute:0,
        Seconds:0,
        Remseconds:0,
        old :''

      }
    },
    mounted() {
      this.old = localStorage.getItem(`page_${this.$route.params.slug}`)
      this.Result = JSON.parse(localStorage.getItem(`Result_${this.$route.params.slug}`));
      console.log("this.Result",this.Result.results)
    },
    methods: {


    },

  }
</script>


<style scoped>

.bg_gray{
  background-color: #E7F0F3;
}
</style>

<template>
  <b-container>
    <b-row align-h="center"  class="flex-wrap-reverse">
    <b-col cols="12"  lg="5" class="text_GraySec m-sec">

      <div class="bgGray rounded_0 p-3 my-4">
        <div class="d-flex justify-content-between">
          <p>الوحدة الاولي: اسم الوحدة</p>
          <img :src="require(`~/assets/icon/downUP.svg`)" v-on:click="Up = !Up" :class="Up === true ? 'd-block downUP' : 'd-none'" alt="icon"/>
          <img :src="require(`~/assets/icon/upDown.svg`)" v-on:click="Up = !Up" :class="Up === false ? 'd-block downUP' : 'd-none'" alt="icon"/>
        </div>

        <div :class="Up === false ? 'd-block' : 'd-none'">
          <div class="d-flex justify-content-between align-items-center my-4">
            <div class="d-flex align-items-center">
              <img :src="require(`~/assets/icon/righte.svg`)" class="iconCheck" alt="icon"/>
              <p class="my-0 mr-2">نص وهمي لدرس الكورس</p>
            </div>
            <p class="my-0">02:30</p>
          </div>

          <div class="d-flex justify-content-between align-items-center my-4">
            <div class="d-flex align-items-center">
              <img :src="require(`~/assets/icon/righte.svg`)" class="iconCheck" alt="icon"/>
              <p class="my-0 mr-2">نص وهمي لدرس الكورس</p>
            </div>
            <p class="my-0">02:30</p>
          </div>

          <div class="d-flex justify-content-between align-items-center my-4">
            <div class="d-flex align-items-center">
              <img :src="require(`~/assets/icon/righte.svg`)" class="iconCheck" alt="icon"/>
              <p class="my-0 mr-2">نص وهمي لدرس الكورس</p>
            </div>
            <p class="my-0">02:30</p>
          </div>

          <div class="d-flex justify-content-between align-items-center my-4">
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
          </div>
        </div>



      </div>

      <div class="bgGray rounded_0 p-3 my-4">
        <div class="d-flex justify-content-between">
          <p>الوحدة الثانية: اسم الوحدة</p>
          <img :src="require(`~/assets/icon/downUP.svg`)" v-on:click="Up_2 = !Up_2" :class="Up_2 === true ? 'd-block downUP' : 'd-none'" alt="icon"/>
          <img :src="require(`~/assets/icon/upDown.svg`)" v-on:click="Up_2 = !Up_2" :class="Up_2 === false ? 'd-block downUP' : 'd-none'" alt="icon"/>
        </div>

        <div :class="Up_2 === false ? 'd-block' : 'd-none'">

          <div class="d-flex justify-content-between align-items-center my-4">
            <div class="d-flex align-items-center">
              <img :src="require(`~/assets/icon/puse.svg`)" class="iconCheck" alt="icon"/>
              <p class="my-0 mr-2">نص وهمي لدرس الكورس</p>
            </div>
            <p class="my-0">02:30</p>
          </div>

          <div class="d-flex justify-content-between align-items-center my-4">
            <div class="d-flex align-items-center">
              <img :src="require(`~/assets/icon/puse.svg`)" class="iconCheck" alt="icon"/>
              <p class="my-0 mr-2">نص وهمي لدرس الكورس</p>
            </div>
            <p class="my-0">02:30</p>
          </div>

          <div class="d-flex justify-content-between align-items-center my-4">
            <div class="d-flex align-items-center">
              <img :src="require(`~/assets/icon/puse.svg`)" class="iconCheck" alt="icon"/>
              <p class="my-0 mr-2">نص وهمي لدرس الكورس</p>
            </div>
            <p class="my-0">02:30</p>
          </div>

        </div>



      </div>

      <div class="bgGray rounded_0 p-3 my-4">
        <div class="d-flex justify-content-between">
          <p>الوحدة الثالثة: اسم الوحدة</p>
          <img :src="require(`~/assets/icon/downUP.svg`)" v-on:click="Up_3 = !Up_3" :class="Up_3 === false ? 'd-block downUP' : 'd-none'" alt="icon"/>
          <img :src="require(`~/assets/icon/upDown.svg`)" v-on:click="Up_3 = !Up_3" :class="Up_3 === true ? 'd-block downUP' : 'd-none'" alt="icon"/>
        </div>

        <div :class="Up_3 === true ? 'd-block' : 'd-none'">

          <div class="d-flex justify-content-between align-items-center my-4">
            <div class="d-flex align-items-center">
              <img :src="require(`~/assets/icon/puse.svg`)" class="iconCheck" alt="icon"/>
              <p class="my-0 mr-2">نص وهمي لدرس الكورس</p>
            </div>
            <p class="my-0">02:30</p>
          </div>

          <div class="d-flex justify-content-between align-items-center my-4">
            <div class="d-flex align-items-center">
              <img :src="require(`~/assets/icon/puse.svg`)" class="iconCheck" alt="icon"/>
              <p class="my-0 mr-2">نص وهمي لدرس الكورس</p>
            </div>
            <p class="my-0">02:30</p>
          </div>

          <div class="d-flex justify-content-between align-items-center my-4">
            <div class="d-flex align-items-center">
              <img :src="require(`~/assets/icon/puse.svg`)" class="iconCheck" alt="icon"/>
              <p class="my-0 mr-2">نص وهمي لدرس الكورس</p>
            </div>
            <p class="my-0">02:30</p>
          </div>

        </div>



      </div>

    </b-col>
    <b-col cols="12"  lg="7" class="m-sec">
      <div class="video">
        <img :src="require(`~/assets/img/Group 1472.png`)" class="img" alt="icon"/>
        <div class="overly">
          <img :src="require(`~/assets/icon/lock.svg`)" class="lock" alt="icon"/>
          <p class="text-white font-16">(متاحة للمشتركين بالدورة الشاملة مثلا)</p>
        </div>
      </div>
      <p class="my-3 font-16">اسم الدورة وعنونها هنا اونلاين<span class="text_yellow"> (متاحة للمشتركين بالدورة الشاملة مثلا)</span></p>

      <div class="shadow rounded_1 p-3 my-3 d-flex flex-wrap">
        <div class="bgfillBlue border-radius fileParent">
          <img :src="require(`~/assets/icon/file22.svg`)" class="file" alt="icon"/>
        </div>
        <div class="mr-3">
          <p class="my-0">ملف محلول</p>
          <p class="text_green mt-1">بحجم 2 ميجا</p>
        </div>
        <div class="mr-auto">
          <img :src="require(`~/assets/icon/pdf.svg`)" class="pdf ml-5" alt="icon"/>
          <b-button size="sm" class="btn btn_blue my-2 py-2 px-5 rounded_0" type="button" > تحميل</b-button>
        </div>
      </div>


      <div class="shadow rounded_1 p-3 my-3 d-flex flex-wrap">
        <div class="bgfillBlue border-radius fileParent">
          <img :src="require(`~/assets/icon/file22.svg`)" class="file" alt="icon"/>
        </div>
        <div class="mr-3">
          <p class="my-0"> ملف غير محلول</p>
          <p class="text_yellow mt-1">بحجم 4 ميجا</p>
        </div>
        <div class="mr-auto">
          <img :src="require(`~/assets/icon/pdf.svg`)" class="pdf ml-5" alt="icon"/>
          <b-button size="sm" class="btn btn_blue my-2 py-2 px-5 rounded_0" type="button" > تحميل</b-button>
        </div>
      </div>

      <div class="orangeLind"></div>


      <div class="shadow rounded_1 p-3 my-3 d-flex flex-wrap">
        <div class="bgfillBlue border-radius fileParent">
          <img :src="require(`~/assets/icon/testfile.svg`)" class="file" alt="icon"/>
        </div>
        <div class="mr-3">
          <p class="my-0"> اختبار الكتروني</p>
          <p class="text_green mt-1">عدد 15 سؤال</p>
        </div>
        <div class="mr-auto">
          <b-button size="sm" class="btn btn_Green my-2 py-2 px-5 rounded_0" type="button" > ابدا الان</b-button>
        </div>
      </div>

      <div class="orangeLind"></div>


      <div class="shadow rounded_1 p-3 my-3 d-flex flex-wrap">
        <div class="bgfillOrange border-radius fileParent">
          <img :src="require(`~/assets/icon/fillornge222.svg`)" class="file" alt="icon"/>
        </div>
        <div class="mr-3">
          <p class="my-0"> ملف التحديثات</p>
          <p class="text_blue mt-1">بحجم 25 ميجا </p>
        </div>
        <div class="mr-auto">
          <img :src="require(`~/assets/icon/pdf.svg`)" class="pdf ml-5" alt="icon"/>
          <b-button size="sm" class="btn btn_yellow my-2 py-2 px-5 rounded_0" type="button" > تحميل</b-button>
        </div>
      </div>


    </b-col>
  </b-row>
  </b-container>
</template>

<script>
  export default {
    data() {
        return {
        Up: false,
        Up_3:false,
        Up_2:false,
      }
    },

  };

  </script>


<style scoped>
  .video{
    position: relative;
  }
  .video .img{
    width: 100% ;
    height: 400px;
  }
  .video .overly{
    position: absolute;
    top: 0;
    width: 100% ;
    height: 400px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
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
</style>

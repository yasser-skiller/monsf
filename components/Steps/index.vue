<template>
    <b-container class="m-sec">
      <b-row align-h="center"  class="flex-wrap align-items-center ">
        <b-col cols="12" sm="10"  lg="5" class="mt-4">
          <h3 class="text_blue font-weight-bold">
            خطوات التسجيل
            <br/>
            في دوراتنا
          </h3>
          <p class="my-3 ml-5">هذا النص هو مثال لنص يمكن أن يستبدل في نفس المساحة، لقد تم توليد هذا النص من مولد</p>
          <button class="btn btn_blue my-2 mx-2 py-2 px-4 rounded_0">احصل عليها الان</button>
        </b-col>
        <b-col cols="12" sm="10" lg="6" class="">

          <div class="d-flex flex-wrap justify-content-between align-items-center">
            <b-col cols="12" sm="10"  lg="6" class="d-flex mt-4">
              <h4 class="text_yellow">01</h4>
              <div class="mr-3">
                <img :src="require(`~/assets/icon/privacy.svg`)" class="icon" alt="icon"/>
                <p class="my-2">قم بتسجيل الدخول الي موقعنا</p>
              </div>
            </b-col>

            <b-col cols="12" sm="10"  lg="6" class="d-flex mt-4">
              <h4 class="text_yellow">02</h4>
              <div class="mr-3">
                <img :src="require(`~/assets/icon/online-course.svg`)" class="icon" alt="icon"/>
                <p class="my-2">اختر الدورة التي  تريدالانضمام اليها</p>
              </div>
            </b-col>

          </div>
          <div class="d-flex flex-wrap justify-content-between align-items-center">

            <b-col cols="12" sm="10"  lg="6" class="d-flex mt-4">
              <h4 class="text_yellow">03</h4>
              <div class="mr-3">
                <img :src="require(`~/assets/icon/course.svg`)" class="icon" alt="icon"/>
                <p class="my-2 w-75">تصفح تفاصيل الدورة التي  قمت باختيارها</p>
              </div>
            </b-col>

            <b-col cols="12" sm="10"  lg="6" class="d-flex mt-4">
              <h4 class="text_yellow">04</h4>
              <div class="mr-3">
                <img :src="require(`~/assets/icon/contacts.svg`)" class="icon" alt="icon"/>
                <p class="my-2">تواصل معنا عن طريق رقم التسجيل عن  طريق تزويده باسم الدورة</p>
              </div>
            </b-col>

          </div>

        </b-col>
      </b-row>
    </b-container>
</template>

<script>
export default {

};

</script>

<style scoped>
.icon{
  width: 40px;
}
</style>

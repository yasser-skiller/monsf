<template >
  <div class="bgDark m-sec">
    <b-container class="text-white p-5">
      <img :src="require(`~/assets/icon/logoWhite.svg`)" class="logo" alt="icon"/>

      <b-row align-h="center"  class="flex-wrap align-items-center ">
        <b-col cols="12" sm="10"  lg="6" class="">
          <p class="title">قم بتحسين مهارتك مع المنصف</p>
          <p class="my-4">كل الحقوق محفوظة الي المنصف 2022</p>
        </b-col>
        <b-col cols="12" sm="10" lg="6" class="d-flex flex-wrap align-items-start ">
          <b-col cols="12" sm="10" md="4" lg="4" class="">
            <p class="my-4">روابط سريعة</p>
            <p class="my-3"> الكورسات</p>
            <p class="my-3"> خطوات التسجيل</p>
            <p class="my-3"> تواصل معنا</p>
          </b-col>
          <b-col cols="12" sm="10" md="4" lg="4" class="">
            <p class="my-4"> كورسات المنصف</p>
            <p class="my-3"> الكورس الاول</p>
            <p class="my-3"> الكورس الثاني </p>
            <p class="my-3">  انشاء حساب</p>
          </b-col>
          <b-col cols="12" sm="10" md="4" lg="4" class="">
            <p class="my-3 text-center">  التواصل الاجتماعي</p>
            <div class="d-flex justify-content-between px-4">
              <a><img :src="require(`~/assets/icon/linkedin.svg`)" class="icon" alt="icon"/></a>
              <a><img :src="require(`~/assets/icon/twitter.svg`)" class="icon" alt="icon"/></a>
            </div>
            <div class="d-flex justify-content-between px-4 mt-4">
              <a><img :src="require(`~/assets/icon/youtube.svg`)" class="icon" alt="icon"/></a>
              <a><img :src="require(`~/assets/icon/facebook.svg`)" class="icon" alt="icon"/></a>
            </div>
          </b-col>

        </b-col>
      </b-row>
    </b-container>
  </div>

</template>

<script>
export default {

};

</script>

<style scoped>
.logo{
  width: 90px;
}
.icon{
  width: 20px;
}
.title{
  font-size: 40px;
}

</style>

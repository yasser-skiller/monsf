<template>
  <b-container class="">
    <b-row align-h="center"  class="flex-wrap">

      <b-col cols="12"  lg="6" class="m-sec animate__animated animate__fadeInRight">
        <p class="mt-5">من المنصف</p>
        <h3 class="text_blue">المنصف في القدرات</h3>
        <img :src="require(`~/assets/icon/pathooo.svg`)" class="my-3 w-50" alt="icon"/>
        <p>اولي خطوات النجاح تبدأ معنا</p>
        <p>لدينا الكثير من الطلاب حول العالم. انضم اليهم الآن</p>

        <div class="d-flex bgfillBlue border_blue pr-3 pl-5 py-2 mt-5">
          <img :src="require(`~/assets/icon/logoblue.svg`)" class="icon" alt="icon"/>
          <p class="my-0 mr-4 text_blue">أستاذ محمود المنصف</p>
        </div>
        <div class="d-flex bgfillGreen border_Green pr-3 pl-5 py-2 mt-5">
          <img :src="require(`~/assets/icon/computer.svg`)" class="icon_0" alt="icon"/>
          <p class="my-0 mr-4 text_green">مجموعة كبيرة من الدورات</p>
        </div>
        <div class="d-flex bgfillOrange border_orange pr-3 pl-5 py-2 mt-5">
          <img :src="require(`~/assets/icon/premium-badge.svg`)" class="icon_0" alt="icon"/>
          <p class="my-0  mr-4 text_yellow">دورات عالية الجودة</p>
        </div>
      </b-col>
      <b-col cols="12"  lg="6" class="m-sec d-flex justifiy-content-left animate__animated animate__fadeInLeft">
        <img :src="require(`~/assets/img/Group 1467.png`)" class="img" alt="icon"/>
      </b-col>
    </b-row>
  </b-container>
</template>

<style scoped>
.icon{
  width: 30px;
}
.icon_0{
  width: 20px;
}
.img{
  width: 90%;
  height: 100%;
}
</style>

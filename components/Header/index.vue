<template>
    <b-container class="">
      <b-row align-h="center"  class="flex-wrap align-items-center ">
        <b-col cols="12" lg="4" class="mt-5">
          <div class="position-relative w-100">
            <img :src="require(`~/assets/icon/path.svg`)" class="path" alt="icon"/>
            <h2 class="text_blue">
              المنصف في القدرات
              <br/>
              طريق مضمون لمستقبلك
            </h2>
          </div>

          <p class="text_Gray mt-3">المنصف فى القدرات هو دليلك الأول والأخير لضمان النجاح والتفوق ابدا معنا الان وحقق نجاحك</p>
          <div class="d-flex m-sec">
            <b-button  v-b-modal.modal-1  size="sm" class="btn_blue my-2  mx-2 py-3 px-5 rounded_0" type="button" >ابدا الان</b-button>
            <b-button size="sm" class="my-3 my-sm-2 mx-2 py-3 px-5 rounded_0" type="button" variant="outline-warning" >تسجيل دخول</b-button>
          </div>

        </b-col>
        <b-col cols="12" lg="8" class="position-relative mt-5">
          <img :src="require(`~/assets/img/header.png`)" class="header_img" alt="icon"/>
          <div class="boxTop">
            <p class="text-center text-white m-0">كورسات المنصف</p>
          </div>
          <div class="bord border shadow">
            <div class="d-flex">
              <div class="p-2 rounded_0 ml-3 bgGray"><img :src="require(`~/assets/icon/books.svg`)" class="icon_9" alt="icon"/></div>
              <div>
                <span class="text_blue">الكورس الاول</span>
                <small class="text_green">يوجد خصم عليها الان</small>
                <div class="d-flex mt-2">
                  <p class="my-0 mx-2">عن 2520 تقييم</p>
                  <img :src="require(`~/assets/icon/star2.svg`)" />
                </div>
              </div>

            </div>
            <div class="d-flex mt-4">
              <div class="p-2 rounded_0 ml-3 bgGray"><img :src="require(`~/assets/icon/online-learning.svg`)" class="icon_9" alt="icon"/></div>
              <div>
                <span class="text_blue">الكورس الثاني</span>
                <div class="d-flex mt-2">
                  <p class="my-0 mx-2">عن 2520 تقييم</p>
                  <img :src="require(`~/assets/icon/star2.svg`)" />
                </div>
              </div>

            </div>

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
.path{
  position: absolute;
  top: -20px;
  left: 50px;
  width: 30px;
}
.boxTop{
  position: absolute;
  bottom: 180px;
  right: 465px;
  background-color:#19313A;
  border-radius: 10px;
  padding: 12px 30px;
  z-index: 3;
}
.bord{
  position: absolute;
  bottom: 0px;
  right: 400px;
  background-color: #fff;
  border-radius: 15px;
  padding: 30px 20px;
}
.header_img{
  width: 100%;
}
.icon_9{
  width: 35px;
}
@media (max-width:1200px) {
  .path{
   left: 0px;
  }
}
@media (max-width:989px) {
  .path{
   left: 380px;
  }
}
@media (max-width:767px) {
  .path{
   left: 200px;
  }
  .boxTop{
  position: relative;
  bottom: 85px;
  right: 0px;
  background-color:#19313A;
  border-radius: 10px;
  padding: 12px 30px;
  z-index: 3;
  width: fit-content;
  margin: auto;
}
.bord{
  position: relative;
  bottom: 100px;
  right: 0px;
  background-color: #fff;
  border-radius: 15px;
  padding: 30px 20px;
}
}
@media (max-width:520px) {
  .path{
   left: 20px;
  }
}
</style>

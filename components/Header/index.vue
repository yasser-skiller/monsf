<template>
    <b-container class="">
      <b-row align-h="center"  class="flex-wrap-reverse align-items-center ">
        <b-col cols="12" lg="4" class="mt-5 ">
          <div class="position-relative w-100  animate__fadeInRight">
            <img :src="require(`~/assets/icon/path.svg`)" class="path" alt="icon"/>
            <h3 class="text_blue font-weight-bold">
              المنصف في القدرات
              طريق مضمون لمستقبلك
            </h3>
          </div>

          <p class="text_Gray mt-3">المنصف فى القدرات هو دليلك الأول والأخير لضمان النجاح والتفوق ابدا معنا الان وحقق نجاحك</p>
          <div class="d-flex m-sec">
            <b-button  v-b-modal.modal-1  size="sm" class="btn_blue my-3 my-sm-2  mx-2 py-3 px-5 ppp rounded_0" type="button" >ابدا الان</b-button>
            <b-button size="sm" class="btn btn_yellow my-3 my-sm-2 mx-2 py-3 px-5 rounded_0" type="button" variant="outline-warning" >تسجيل دخول</b-button>
          </div>

          <img :src="require(`~/assets/icon/logooo.svg`)" class="logooo" alt="icon"/>

        </b-col>
        <b-col cols="12" lg="8" class="position-relative m-sec ">
          <img :src="require(`~/assets/img/header.png`)" class="header_img  animate__fadeInLeft" alt="icon"/>
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
  import 'animate.css';
export default {

};

</script>

<style scoped>
.path{
  position: absolute;
  top: -20px;
  left: 10px;
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
.logooo{
  width: 120px;
  margin-top: 50px;
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
   left: 90px;
  }
  .logooo{
    display: none;
  }

}
@media (max-width:767px) {
  .ppp{
    padding: 15px 20px !important;
  }
  .path{
   left: 70px;
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

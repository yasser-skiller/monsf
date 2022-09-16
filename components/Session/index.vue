<template>
   <b-container>
    <b-row align-h="center"  class="flex-wrap">
      <b-col cols="12"  lg="7" class="m-sec">
        <div class="position-relative w-100">
          <img :src="require(`~/assets/icon/path.svg`)" class="path" alt="icon"/>
          <h3 class="text_blue">
            دورة التأسيس (مسجلة)
          </h3>
        </div>

        <h6 class="text_yellow my-4">300 ر.س</h6>
        <p>فيديو شرح للدورة</p>

        <div class="video">
          <img :src="require(`~/assets/img/Group 1478.png`)" class="img" alt="icon"/>
          <div class="overly">
            <img :src="require(`~/assets/icon/pusecircle.svg`)" class="lock" alt="icon"/>
          </div>
        </div>

      </b-col>
      <b-col cols="12"  lg="5" class="m-sec">

        <div class="d-flex flex-column justify-content-left align-items-end">
          <div class="d-flex justify-content-left mb-4">
            <div class="d-flex ">
              <img :src="require(`~/assets/icon/starw.svg`)" class="star" alt="icon"/>
              <img :src="require(`~/assets/icon/starw.svg`)" class="star" alt="icon"/>
              <img :src="require(`~/assets/icon/starw.svg`)" class="star" alt="icon"/>
              <img :src="require(`~/assets/icon/starw.svg`)" class="star" alt="icon"/>
              <img :src="require(`~/assets/icon/starw.svg`)" class="star" alt="icon"/>
            </div>
            <p class="my-0">(5.0)</p>

          </div>
          <b-button type="button" class="btn btn_Green rounded_0 px-5 py-2 w-75"> شراء الدورة الان</b-button>
        </div>
        <p class="mt-5">:يتضمن البرنامج التدريبي</p>

        <div class="d-flex bgfillBlue border_blue_2 pr-3 pl-5 py-2 mt-5 font-16">
          <img :src="require(`~/assets/icon/Time Circle 1.svg`)" class="icon ml-4" alt="icon"/>
          <span>التوقيت  :</span>
          <span class="text_blue mr-3">ساعة و 45 دقيقة</span>
        </div>

        <div class="d-flex bgfillGreen border_Green_2 pr-3 pl-5 py-2 mt-5 font-16">
          <img :src="require(`~/assets/icon/com.svg`)" class="icon ml-4" alt="icon"/>
          <span>المستوي:</span>
          <span class="text_green mr-3">مهارات التأسيس</span>
        </div>

        <div class="d-flex bgfillOrange border_orange_2 pr-3 pl-5 py-2 mt-5 font-16">
          <img :src="require(`~/assets/icon/des.svg`)" class="icon ml-4" alt="icon"/>
          <span>المحاضرات:</span>
          <span class="text_yellow mr-3">عدد 19 محاضرة</span>
        </div>

        <div class="d-flex bgfillRed border_red_2 pr-3 pl-5 py-2 mt-5 font-16">
          <img :src="require(`~/assets/icon/icons Q2.svg`)" class="icon ml-4" alt="icon"/>
          <span class="text_red mr-3">تم تسجيل اكثر من 1000 طالب</span>
        </div>

        <div class="d-flex  mt-5 font-16">
          <img :src="require(`~/assets/img/Ellipse 970.png`)" class="person ml-3" alt="icon"/>
          <div>
            <p class="my-0 mt-1 text_Gray">المدرس</p>
            <p class="my-0 mt-1">الأستاذ: محمد المنصف</p>
          </div>
        </div>

      </b-col>

      <div class="my-4 text-right">
        <p class="font-16 ">لمحة عن الدورة</p>
        <div class="GrayLine bgGray">
          <div class="GreenLine bgGreen"></div>
        </div>
        <p class="text_GraySec mt-3">
          هذا النص هو مثال لنص يمكن أن يستبدل في نفس المساحة، لقد تم توليد هذا النص من مولد النص العربى، حيث يمكنك أن تولد مثل هذا النص أو العديد من النصوص الأخرى إضافة إلى زيادة عدد الحروف التى يولدها التطبيق. إذا كنت تحتاج إلى عدد أكبر من الفقرات يتيح لك مولد النص العربى
        </p>
      </div>


    </b-row>
  </b-container>
</template>

<style scoped>
 .path{
    position: absolute;
    top: -20px;
    right: 280px;
    width: 40px;
  }
  .video{
    position: relative;
  }
  .video .img{
    width: 100% ;
    height: 350px;
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
  .GrayLine{
    width: 100%;
    height: 3px;
    position: relative;
  }
  .GreenLine{
    border-radius: 5px   5px 0 0;
    width: 10%;
    height: 9px;
    position:absolute ;
    top: -5px;
  }
  .person{
    width: 60px;
    height: 60px;
    border-radius: 50%;
  }
  .star{
    width: 20px;
    margin: 0 5px;
  }
  .justify-content-left{
    justify-content: left !important;
  }
</style>

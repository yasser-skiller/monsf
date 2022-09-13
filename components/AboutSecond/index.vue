<template>
  <b-container class="mb-5">
    <b-row align-h="center"  class="flex-wrap">

      <b-col cols="12"  lg="6" class="m-sec animate__animated animate__fadeInRight">

        <div class="mb-5 position-relative">
          <img :src="require(`~/assets/icon/logoblue.svg`)" class="icon" alt="icon"/>
          <img :src="require(`~/assets/icon/pathblue.svg`)" class="path_0" alt="icon"/>
          <p class="mt-3 mb-4 font-16 font-weight-bold text_blue">أستاذ محمود المنصف</p>
          <p>
            المنصف فى القدرات .. لضمان الحصول على ال 100% ومن السمات الرئيسية فى الدورات هى
القدرة على تطوير العلاقات مع الطلاب،والمعرفة اللطيفة التي تقدم للمتعلم .
          </p>
        </div>
        <div class="my-5 position-relative">
          <img :src="require(`~/assets/icon/computer.svg`)" class="icon_0" alt="icon"/>
          <img :src="require(`~/assets/icon/pathgreen.svg`)" class="path_1" alt="icon"/>
          <p class="mt-3 mb-4 font-16 font-weight-bold text_green">مجموعة كبيرة من الدورات</p>
          <p>
            لضمان الحصول على ال 100% وضمان التفوق والنجاح والتدريب المستمر على الإختبارات والكورسات
المتنوعه هو الإشتراك فى دورات المنصف .. مع وجود دورات للبنين والبنات منفصله
          </p>
        </div>
        <div class="my-5 position-relative">
          <img :src="require(`~/assets/icon/premium-badge.svg`)" class="icon_0" alt="icon"/>
          <img :src="require(`~/assets/icon/pathyellow.svg`)" class="path_2" alt="icon"/>
          <p class="mt-3 mb-4 font-16 font-weight-bold text_yellow">دورات عالية الجودة</p>
          <p>
            يتمتع المنصف فى القدرات بالقدره على توصيل المعلومه بإنسيابيه وسهوله لضمان فهم جميع الطلاب ...
مع اختباارات على كل درس لضمان التدريب والمراجعات الشامله أول بأول مع فكره وجود الدعم لجميع
الطلاب بشكل مستمر وعلى مدار 24 ساعة
          </p>
        </div>
      </b-col>
      <b-col cols="12"  lg="6" class="m-sec d-flex justifiy-content-left animate__animated animate__fadeInLeft">
        <img :src="require(`~/assets/img/Group 1469.png`)" class="img" alt="icon"/>
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
  width: 100%;
  height: 100%;
}
.path_0{
  position: absolute;
  top: 30px;
  right: 150px;
}
.path_1{
  position: absolute;
  top: 30px;
  right: 180px;
}
.path_2{
  position: absolute;
  top: 30px;
  right: 130px;
}

</style>

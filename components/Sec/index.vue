<template>
    <b-container class="m-sec">
      <b-row align-h="center"  class="flex-wrap align-items-center">
        <b-col cols="12" sm="10"  lg="6" class="">
          <div class="pr-5 mb-5">
            <div class="bluebg rounded_0 py-4 px-4">
              <div class="d-flex">
              <img :src="require(`~/assets/img/Content-Round-Gray-Icone.png`)" class="person" alt="icon"/>
              <div class="mr-2">
                <p class="text-white my-1">محمد مصطفي علي</p>
                <small class="color_2">الرياض, السعودية</small>
              </div>
              </div>
              <p class="text-white">هذا النص هو مثال لنص يمكن أن يستبدل في نفس المساحة، لقد تم توليد هذا النص من مولد النص العربى</p>
              <div class="d-flex justify-content-left w-100">
                <b-button size="sm" type="button" class="btn_blue_sp mx-2 px-4 py-2 rounded_0">عرض التجربة</b-button>
              </div>
            </div>
          </div>

          <div class="pl-5">
            <div class="bgGray rounded_0 py-4 px-5">
              <div class="d-flex">
                <img :src="require(`~/assets/img/Content-Round-Gray-Icon.png`)" class="person" alt="icon"/>
                <div class="mr-2">
                  <p class="color_1 my-1">محمد مصطفي علي</p>
                  <small class="color_2">الرياض, السعودية</small>
                </div>
              </div>
              <p class="color_0">هذا النص هو مثال لنص يمكن أن يستبدل في نفس المساحة، لقد تم توليد هذا النص من مولد النص العربى</p>
            </div>
          </div>

        </b-col>
        <b-col cols="12" sm="10" lg="6" class="px-5">
          <h3 class="px-5">يمكنك الاطلاع علي درجاتنا</h3>
          <p class="text_Gray px-5">المنصف فى القدرات .. طريقك إلى ال100% ... أفضل الدورات والدروس والمرجعات الشاملة</p>
          <b-button size="sm" type="button" class="btn_blue m-sec mx-2 p-3 mx-5 rounded_0">الاطلاع علي درجاتنا</b-button>
        </b-col>
      </b-row>
    </b-container>
</template>

<script>
export default {

};

</script>

<style scoped>
.color_0{
  color: #5C5C5C;
}
.color_1{
  color: #232323;
}
.color_2{
  color: #969696;
}
.person{
  width: 60px;
  height: 60px;
  border-radius: 50%;
}
.justify-content-left{
  justify-content: left
}
</style>

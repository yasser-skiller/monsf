<template>
    <b-container class="m-sec">
      <b-row align-h="center"  class="flex-wrap align-items-center rounded_1 bgGray">
        <b-col cols="12" sm="10"  lg="5" class="mt-4 pb-2">
          <h3 class="text_blue">جرب اختبارت المنصف</h3>
          <p class="mt-4 mb-5">هذا النص هو مثال لنص يمكن أن يستبدل في نفس المساحة، لقد تم توليد هذا النص من مولد النص العربى، حيث يمكنك أن تولد مثل هذا النص أو العديد من النصوص الأخرى إضافة إلى زيادة عدد الحروف التى يولدها التطبيق</p>
          <b-button size="sm" type="button" class="btn_blue mt-2 mb-5  mx-2 py-3 px-5 rounded_0">جرب الان</b-button>
        </b-col>
        <b-col cols="12" sm="10" lg="7" class="bg">
          <img :src="require(`~/assets/img/sec.png`)" class="sec" alt="icon"/>
        </b-col>
      </b-row>
    </b-container>
</template>

<script>
export default {

};

</script>

<style scoped>
.bg{
  position: relative;
  background-image: url('./../../assets/img/bg_logo.png');
  background-position: center;
  background-repeat:repeat-y repeat-x;
  background-size: cover;
  width: 100%;
  height: 200px;
  display: flex;
  justify-content: center;
}
.sec{
  position: absolute;
  top: -120px;
  width: 500px;
}
@media (max-width:989px) {
  .sec{
    top: -60px;
    width: 400px;
  }
}
@media (max-width:567px) {
  .sec{
    top: -20px;
    width: 300px;
  }
}
</style>

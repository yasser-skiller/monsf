<template>
    <b-container class="m-sec">
      <b-row align-h="center"  class="flex-wrap align-items-center rounded_1 bgGray">
        <b-col cols="12" sm="10"  lg="6" class="bg text-white p-5">
          <h3>تواصل معنا الان</h3>
          <p class="mt-4">هذا النص هو مثال لنص يمكن أن يستبدل في نفس المساحة، لقد تم توليد هذا النص من مولد النص العربى، حيث يمكنك أن تولد مثل هذا النص</p>
          <h6 class="m-sec mb-4"> بيانات التواصل : </h6>
          <div class="d-flex align-items-center ">
            <span class="mark"></span>
            <span>01033143665</span>
          </div>
          <div class="d-flex align-items-center ">
            <span class="mark"></span>
            <span>البريد الالكتروني</span>
          </div>
          <div class="d-flex align-items-center ">
            <span class="mark"></span>
            <span>العنوان</span>
          </div>

        </b-col>
        <b-col cols="12" sm="10" lg="6" class="bgGray">

        </b-col>
      </b-row>
      <div class="m-sec">r</div>
    </b-container>
</template>

<script>
export default {

};

</script>

<style scoped>
.bg{
  position: relative;
  background-image: url('./../../assets/img/cal.png');
  background-position: center;
  background-repeat:repeat-y repeat-x;
  background-size: cover;
  width: 100%;
}
.mark{
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background-color: var(--GrayColor);
  margin: 10px 0 10px 10px;
}

</style>

<template>
    <b-container class="m-sec">
      <b-row align-h="center"  class="flex-wrap align-items-center ">
        <b-col cols="12" sm="10"  lg="4" class="mt-4">
          <h4 class="text_blue font-weight-bold">
            افضل اختيار ودورات
            <br/>
            للتعلم اونلاين علي الانترنت
          </h4>
        </b-col>
        <b-col cols="12" sm="10" lg="8" class="d-flex flex-wrap justify-content-between">
          <div class="mt-4">
            <img :src="require(`~/assets/icon/bronze-medal.svg`)" class="icon" alt="icon"/>
            <p class="text_green font-16 my-2 font-weight-bold">تحصل عالـ 100 معنا بإذن الله </p>
            <p class="my-2">
              دوراتنا هي الأفضل لك وتساعدك
              <br/>
              علي تحقق نجاحك
            </p>
          </div>
          <div class="mt-4">
            <img :src="require(`~/assets/icon/strategy.svg`)" class="icon" alt="icon"/>
            <p class="text_green font-16 my-2 font-weight-bold">إستراتيجيات الحل</p>
            <p class="my-2">
              نعطيك أسرع وأسهل
              <br/>
              الطرق لحل الأسئلة
            </p>
          </div>
          <div class="mt-4">
            <img :src="require(`~/assets/icon/working-hours.svg`)" class="icon" alt="icon"/>
            <p class="text_green font-16 my-2 font-weight-bold">اختصار الوقت</p>
            <p class="my-2">
              تعطيك دوراتنا سرعة في الحل عن طريق
              <br/>
              طرق سهلة لحل الأسئلة
            </p>
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

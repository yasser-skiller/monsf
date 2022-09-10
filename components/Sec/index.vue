<template>
    <b-container class="m-sec">
      <b-row align-h="center"  class="flex-wrap-reverse align-items-center">
        <b-col cols="12" sm="10"  lg="6" class=" mt-5 animate__animated animate__fadeInRight">
          <div class="d-flex">

            <div>
              <div class="pr-5 mb-5">
            <div class="bluebg rounded_0 py-4 px-4">
              <div class="d-flex">
              <img :src="Double === true ? require(`~/assets/img/Content-Round-Gray-Icon.png`) : require(`~/assets/img/Content-Round-Gray-Icone.png`)" :class="Double === false ? 'person slow': 'person slow2'" alt="icon"/>
              <div class="mr-2">
                <p :class="Double === false ? 'text-white my-1 slow': 'text-white my-1 slow2'" >محمد مصطفي علي</p>
                <small :class="Double === false ? 'color_2 slow':'color_2 slow2'">{{Double === false ? 'الرياض, السعودية' : 'جدة, السعودية'}}</small>
              </div>
              </div>
              <p :class="Double === false ? 'text-white slow': 'text-white slow2'">هذا النص هو مثال لنص يمكن أن يستبدل في نفس المساحة، لقد تم توليد هذا النص من مولد النص العربى</p>
              <div class="d-flex justify-content-left w-100">
                <b-button size="sm" type="button" class="btn_blue_sp mx-2 px-4 py-2 rounded_0">عرض التجربة</b-button>
              </div>
            </div>
              </div>

              <div class="pl-5">
                <div  class="bgGray rounded_0 py-4 px-5">
                  <div class="d-flex">
                    <img :src="Double === true ? require(`~/assets/img/Content-Round-Gray-Icone.png`) : require(`~/assets/img/Content-Round-Gray-Icon.png`)" :class="Double !== false ? 'person slow': 'person slow2'" alt="icon"/>
                    <div class="mr-2">
                      <p :class="Double !== false ? 'color_1 my-1 slow': 'color_1 my-1 slow2'" >محمد مصطفي علي</p>
                      <small :class="Double !== false ? 'color_2 slow': 'color_2 slow2'">{{Double === true ? 'الرياض, السعودية' : 'جدة, السعودية'}}</small>
                    </div>
                  </div>
                  <p :class="Double !== false ? 'color_0 slow': 'color_0 slow2'">هذا النص هو مثال لنص يمكن أن يستبدل في نفس المساحة، لقد تم توليد هذا النص من مولد النص العربى</p>
                </div>
              </div>
            </div>

            <div class="m-sec mr-5">
              <img :src="require(`~/assets/icon/arr.svg`)" v-on:click="Double = !Double" class="arrow" alt="icon"/>
              <br/>
              <br/>
              <img :src="require(`~/assets/icon/arr2.svg`)" v-on:click="Double = !Double" class="arrow" alt="icon"/>
            </div>

          </div>


        </b-col>
        <b-col cols="12" sm="10" lg="6" class="px-5 animate__animated animate__fadeInLeft">
          <div class="line"></div>
          <h3 class="px-5 font-weight-bold">يمكنك الاطلاع علي درجاتنا</h3>
          <p class="text_Gray px-5">المنصف فى القدرات .. طريقك إلى ال100% ... أفضل الدورات والدروس والمرجعات الشاملة</p>
          <b-button size="sm" type="button" class="btn_blue mt-5 mx-2 p-3 mx-5 rounded_0">الاطلاع علي درجاتنا</b-button>
        </b-col>
      </b-row>
    </b-container>
</template>

<script>
export default {
  data() {
      return {
      Double: false,
    }
  },

};

</script>

<style scoped>
.line{
  background-color: var(--GreenColor);
  width: 90px;
  height: 3px;
  margin-right: 3rem;
  margin-bottom: 1.5rem;
}
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
.arrow{
  width:25px;
  cursor: pointer;
}
.slow2{
  animation: fadeInFromNone2 0.5s ease-out;
}
@keyframes fadeInFromNone2 {
    0% {
        opacity: .1;
    }
    25% {
        opacity: .26;
    }
    50% {
        opacity: .6;
    }
    75% {
        opacity: .8;
    }

    100% {
        opacity: .99;
    }
}
.slow{
  animation: fadeInFromNone 0.5s ease-out;
}
@keyframes fadeInFromNone {
  0% {
        opacity: .1;
    }
    25% {
        opacity: .25;
    }
    50% {
        opacity: .5;
    }
    75% {
        opacity: .75;
    }

    100% {
        opacity: 1;
    }
}
</style>

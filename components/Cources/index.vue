<template>
    <b-container class="m-sec">
      <h5 class="font-weight-bold">كورسات المنصف</h5>
      <b-row align-h="center"  class="flex-wrap align-items-center">
        <b-col cols="10" sm="10" md="8"  lg="6" class="mb-4 py-2 px-4">
          <div class="parent">
            <img :src="require(`~/assets/img/Rectangle 613.png`)" class="w-100" alt="icon"/>
            <div class="overly">
              <div class="d-flex bgGreen my-2 mx-2 p-2 rounded_0" >
                <img :src="require(`~/assets/icon/share.svg`)" class="icon" alt="icon"/>
              </div>
              <div class="d-flex bgYellow m-2 p-2  rounded_0" >
                <img :src="require(`~/assets/icon/star.svg`)" class="icon" alt="icon"/>
                <span class="text-white mr-1">(5.0)</span>
              </div>

            </div>
          </div>
          <p class="text_blue mt-2">عنوان الكورس الأول هنا</p>
          <div class="d-flex align-items-center ">
            <img :src="require(`~/assets/icon/book.svg`)" class="icon" alt="icon"/>
            <p class="mr-2 my-0">تحتوي علي 18 درس</p>
          </div>
          <div class="d-flex align-items-center my-3">
            <img :src="require(`~/assets/icon/price-tag.svg`)" class="icon" alt="icon"/>
            <p class="mr-2 my-0">300 ر.س</p>
          </div>
        </b-col>
        <b-col cols="10" sm="10" md="8"  lg="6" class="mb-4 py-2 px-4">
          <div class="parent">
            <img :src="require(`~/assets/img/Rectangle 613.png`)" class="w-100" alt="icon"/>
            <div class="overly">
              <div class="d-flex bgGreen my-2 mx-2 p-2 rounded_0" >
                <img :src="require(`~/assets/icon/share.svg`)" class="icon" alt="icon"/>
              </div>
              <div class="d-flex bgYellow m-2 p-2  rounded_0" >
                <img :src="require(`~/assets/icon/star.svg`)" class="icon" alt="icon"/>
                <span class="text-white mr-1">(5.0)</span>
              </div>

            </div>
          </div>
          <p class="text_blue mt-2">عنوان الكورس الأول هنا</p>
          <div class="d-flex align-items-center ">
            <img :src="require(`~/assets/icon/book.svg`)" class="icon" alt="icon"/>
            <p class="mr-2 my-0">تحتوي علي 18 درس</p>
          </div>
          <div class="d-flex align-items-center my-3">
            <img :src="require(`~/assets/icon/price-tag.svg`)" class="icon" alt="icon"/>
            <p class="mr-2 my-0">300 ر.س</p>
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
.parent{
  position: relative;
}
.overly{
  position: absolute;
  top: 0;
  bottom: 0;
  right: 0;
  left: 0;
  background-image: url('~/assets/img/Rectangle 45.png');
  width: 100%;
  display: flex;
  justify-content: end;
  align-items: flex-start;
}
.icon{
  width: 15px;
}
</style>

<template>
    <b-navbar toggleable="lg"  class="mx-3 fixed bg-white w-100" >

    <b-navbar-brand href="#">
      <div  class="d-flex align-items-center">
        <img :src="require(`~/assets/icon/logo.svg`)" class="logo" alt="icon"/>
      </div>
    </b-navbar-brand>
        <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>


    <b-collapse id="nav-collapse" class="justify-content-between" is-nav>

      <b-navbar-nav class="pr-0 NavBar mr-5  text-center justify-content-between align-items-center">
        <NuxtLink  to="/" tag="li" exact class="nav-link" >الرئيسية</NuxtLink >
        <NuxtLink to="#2" class="nav-link"> الكورسات</NuxtLink>
        <NuxtLink to="#3" class="nav-link">لماذا المنصف</NuxtLink>
        <NuxtLink to="#4" class="nav-link">عن المنصف</NuxtLink>
        <NuxtLink to="#5" class="nav-link"> خطوات التسجيل</NuxtLink>
        <NuxtLink to="#6" class="nav-link">تواصل معنا</NuxtLink>
      </b-navbar-nav>

      <b-navbar-nav class="pr-0">
        <div class="d-flex btns">
          <b-button   size="sm" class="search_btn my-2 my-sm-2 mx-2 py-2 px-3 rounded_0" type="button" > <img :src="require(`~/assets/icon/search.svg`)" alt="icon"/></b-button>
          <b-button size="sm" class="my-2 my-sm-2 mx-2 py-2 px-4 rounded_0" type="button" variant="outline-warning" >تسجيل دخول</b-button>
        </div>

        <!-- <b-button  v-b-modal.modal-1  size="sm" class="search_btn my-2 my-sm-2 mx-2 py-2 px-3 rounded_0" type="button" > <img :src="require(`~/assets/icon/search.svg`)" alt="icon"/></b-button> -->
        <!-- <b-modal id="modal-1"   hide-footer hide-header>
          <div class="modal_style">
            <b-form @submit="onSubmit" @reset="onReset">
            <b-form-input
              id="input-1"
              v-model="form.search"
              type="search"
              placeholder="Enter search ...."
              required
            ></b-form-input>
            </b-form>
          </div>
        </b-modal> -->
      </b-navbar-nav>

    </b-collapse>

    </b-navbar>
</template>

<script>
export default {
  // data() {
  //     return {
  //       form: {
  //       search: '',
  //     }
  //   }
  // },
  //  methods: {
  //     onSubmit(event) {
  //       event.preventDefault()
  //       alert(JSON.stringify(this.form))
  //     },
  //     onReset(event) {
  //       event.preventDefault()
  //       // Reset our form values
  //       this.form.search = ''
  //     }
  //   }

};

</script>

<style scoped>
.fixed{
  position: fixed;
  z-index: 20000000000;
}
 .logo{
  width: 65px;
  margin-left: 5px;
 }
 .logoText{
   display: flex;
   flex-direction: column;
   font-size: 10px;
 }
 .nav-link{
  margin: 0 15px;
  color: var(--GrayColor) !important;
  cursor: pointer;
 }
 .nav-link:hover{
  color: var(--BlackColor) !important;
 }
 .nuxt-link-active{
   color: var(--DarkBlueColor) !important;
   position: relative;
   display: flex;
   flex-direction: column;
   align-items: center;
 }
 .NavBar .nuxt-link-active::after{
   content: url('~/assets/icon/activeLink.svg');
   position: absolute;
   bottom: -15px;
 }

.modal_style{
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 60vh;
}

@media (max-width:1100px) {
  .nav-link{
    margin: 0 5px
  }
}
@media (max-width:989px) {
  .NavBar{
    margin-right: 0 !important;
  }
  .nav-link{
    margin: 5px 0;
  }
  .btns{
    justify-content: center;
    align-items: center;
  }
}
</style>

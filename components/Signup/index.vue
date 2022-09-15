<template>
  <b-row align-h="center"  class="flex-wrap-reverse">
    <b-col cols="12" lg="6" class=" p-5 pb-0 animate__animated animate__fadeInRight">
      <NuxtLink to="/"  exact>
        <img :src="require(`~/assets/icon/logo.svg`)" class="logo" alt="icon"/>
      </NuxtLink>
      <div class="position-relative">
        <h3 class="my-4 text_blue">مرحبا بك في المنصف</h3>
        <img :src="require(`~/assets/icon/pathgreen.svg`)" class="path_1" alt="icon"/>
      </div>
      <p class="font-16 text_yellow">تسجيل الدخول الي المنصف</p>

      <b-form @submit="onSubmit" class="mt-5">


        <div class="d-flex flex-column position-relative mt-5">
          <label class="label"> الاسم بالكامل</label>
          <input
            id="input"
            v-model="form.name"
            placeholder="محمد مصطفي علي"
            required
          />
        </div>

        <div class="d-flex flex-column position-relative mt-5">
          <label class="label">البريد الالكتروني</label>
          <input
            id="input"
            v-model="form.email"
            placeholder="...اكتب البريد الالكتروني هنا"
            type="email"
            required
          />
        </div>

        <div class="d-flex flex-column position-relative mt-5">
          <label class="label"> رقم الهاتف</label>
          <input
            id="input"
            v-model="form.number"
            placeholder="   ...اكتب رقم الهاتف هنا"
            type="number"
            required
          />
        </div>

        <div class="d-flex flex-column position-relative mt-5">
          <label class="label"> رمز المرور</label>
          <input
            id="input"
            v-model="form.email"
            placeholder="...اكتب رمز المرور"
            type="password"
            required
          />
        </div>


        <div class="mt-5 d-flex justify-content-center">
          <b-button type="submit" class="btn btn_blue rounded_1 px-5 py-2 "> انشاء حساب</b-button>
        </div>
        <div class="d-flex my-2 justify-content-center">
          <p>لديك حساب بالفعل!؟ </p>
          <NuxtLink to="/Login" class=""> تسجيل دخول الان</NuxtLink>
        </div>
      </b-form>

    </b-col>
    <b-col cols="12" md="6" lg="6" class="animate__animated animate__fadeInRight">
      <img :src="require(`~/assets/img/Group 1471.png`)" class="img" alt="icon"/>
    </b-col>
  </b-row>
</template>

<script>
  export default {
    data() {
      return {
        form: {
          email: '',
          password: '',
          number:'',
          name:''
        },
      }
    },
    methods: {
      onSubmit(event) {
        event.preventDefault()
        alert(JSON.stringify(this.form))
        this.form.email = ''
        this.form.password = ''
        this.form.name = ''
        this.form.number = ''

      },

    }
  }
</script>


<style scoped>
.logo{
  width: 70px;
}

.img{
  width: 100%;
}
@media (max-width:989px) {
  .img{
   display: none;
  }
}
.path_1{
  width: 30px;
  position: absolute;
  top: -10px;
  right: 250px;
}

#input{
  padding: 20px 15px;
  background-color: #fff;
  border:1px solid #B7B9CE;
  border-radius: 10px;
  color: #B7B9CE;
  outline: none;

}
#input :focus{
  background-color: #fff;
  border:1px solid #B7B9CE;
  outline: none;
}


.label{
  position: absolute;
  top: -10px;
  right: 30px;
  background-color: #fff;
  width: 140px;
  text-align: center;
}

</style>

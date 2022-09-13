<template>
 <div>
   <AppNav/>
   <About/>
   <AboutSecond/>
   <AppFooter/>
 </div>
</template>

<script>
import AppNav from '@/components/AppNav';
import About from '@/components/About';
import AboutSecond from '@/components/AboutSecond';
import AppFooter from '@/components/AppFooter';

export default {
  components:{
    AppNav,
    About,
    AboutSecond,
    AppFooter,
  },
}
</script>

<template>
 <div>
   <AppNav/>
   <Header/>
   <Info/>
   <Cources/>
   <Steps/>
   <Channel/>
   <Try/>
   <Sec/>
   <Contact/>
   <AppFooter/>
 </div>
</template>

<script>
import AppNav from '@/components/AppNav';
import Header from '@/components/Header';
import Info from '@/components/Info';
import Cources from '@/components/Cources';
import Steps from '@/components/Steps';
import Channel from '@/components/Channel';
import Try from '@/components/Try';
import Sec from '@/components/Sec';
import Contact from '@/components/Contact';
import AppFooter from '@/components/AppFooter';

export default {
  components:{
    AppNav,
    Header,
    Info,
    Cources,
    Steps,
    Channel,
    Try,
    Sec,
    Contact,
    AppFooter,
  },
}
</script>

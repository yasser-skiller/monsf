<template>
 <div>
   <AppNav/>
   <Header/>
   <Info/>
   <Cources/>
   <Steps/>
   <Channel/>
 </div>
</template>

<script>
import AppNav from '@/components/AppNav';
import Header from '@/components/Header';
import Info from '@/components/Info';
import Cources from '@/components/Cources';
import Steps from '@/components/Steps';
import Channel from '@/components/Channel';

export default {
  components:{
    AppNav,
    Header,
    Info,
    Cources,
    Steps,
    Channel,
  },
}
</script>

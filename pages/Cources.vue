<template>
 <div>
   <AppNav/>
   <CourcesPage/>
   <AppFooter/>
 </div>
</template>

<script>
import AppNav from '@/components/AppNav';
import CourcesPage from '@/components/CourcesPage';
import AppFooter from '@/components/AppFooter';

export default {
  components:{
    AppNav,
    CourcesPage,
    AppFooter,
  },
}
</script>

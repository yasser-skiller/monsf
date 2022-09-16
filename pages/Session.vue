<template>
  <div>
    <AppNav/>
    <Session/>
    <AppFooter/>
  </div>
 </template>

 <script>
 import AppNav from '@/components/AppNav';
 import Session from '@/components/Session';
 import AppFooter from '@/components/AppFooter';

 export default {
   components:{
     AppNav,
     Session,
     AppFooter,
   },
 }
 </script>

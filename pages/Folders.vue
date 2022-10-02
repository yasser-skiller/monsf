<template>
  <div>
    <AppNav/>
    <Folders/>
    <AppFooter/>
  </div>
 </template>

 <script>
 import AppNav from '@/components/AppNav';
 import Folders from '@/components/Folders';
 import AppFooter from '@/components/AppFooter';

 export default {
   components:{
     AppNav,
     Folders,
     AppFooter,
   },
 }
 </script>

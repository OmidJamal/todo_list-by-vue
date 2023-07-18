<template>
  <div class="mainNav">
    <router-link :to="{name: 'home'}">لیست</router-link>
    <router-link :to="{name: 'AddProject'}"> اضافه کردن لیست کاری جدید</router-link>
  </div>
</template>

<script>
export default {

}
</script>

<style>
    .mainNav{
        text-align: center;
        margin: 40px auto;
    }
    .mainNav a{
        display: inline-block;
        text-decoration: none;
        margin: 0 10px;
        color: #999;
        font-size: 18px;
    }
    a.router-link-active{
        border-bottom: 2px solid #00ce89;
        padding-bottom: 4px;
    }
</style>
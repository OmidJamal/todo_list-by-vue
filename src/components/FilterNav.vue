<template>
  <nav class="filterNav">
    <button @click="uodateFiler('all')" :class="{active: current==='all'}">نمایش همه</button>
    <button @click="uodateFiler('completed')" :class="{active: current==='completed'}">تکمیل شده ها</button>
    <button @click="uodateFiler('ongoing')" :class="{active: current==='ongoing'}">ناتمام</button>
  </nav>
</template>

<script>
export default {
    props:['current'],
    methods: {
        uodateFiler(by){
            this.$emit('filterChange', by)
        }
    }
}
</script>

<style>
    .filterNav button{
        background: none;
        border: none;
        color: #bbb;
        outline: none;
        font-size: 12px;
        text-transform: uppercase;
        margin-right: 10px;
        letter-spacing: 1px;
        font-weight: bold;
        cursor: pointer;
    }
    .filterNav button.active{
        color: #555;
    }
</style>
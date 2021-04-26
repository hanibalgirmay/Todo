<template>
  <div>
      <div v-for="(i,index) in items" :key="index">
          <Item :item="i" class="item" @v-on:itemchanged="$emit('reloadlist')" />
      </div>
  </div>
</template>

<script>
import Item from './listItem';

export default {
     props:["items"],
     components:{Item}
}
</script>

<style>
.item{
    background:#e568a3;
    padding:5px;
    margin-top:5px;
}
</style>

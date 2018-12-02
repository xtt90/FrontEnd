<template>
  <div>
    <!-- <h1>商品sdd组件</h1> -->
    <cmtbox :id="$route.params.id"></cmtbox>
  </div>
</template>

<script>
    import cmtbox from '../subcomponents/comment.vue'
    export default{
      components :{
        cmtbox
      }
    }
</script>

<style>

</style>

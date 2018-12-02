<template>
  <div class="goodsinfo-container">
    <!-- <h1>商品组件</h1> -->
    <h3>{{ info.title }}</h3>
    <hr>
    <div class="content" v-html="info.content"></div>
  </div>
</template>

<script>
    export default{
      data(){
        return {
          id: this.$route.params.id,
          info:{}
        }
      },
      created(){
        this.getGoodsDesa()
      },
      methods:{
        getGoodsDesa(){
          this.$http.get('api/goods/getdesc/'+ this.id).then(result=>{
            // console.log(result.body);
            // console.log(this.id);
             if(result.body.status===0){
              this.info = result.body.message[0];
            }
          })
        }
      }
    }
</script>

<style lang="less" >
.goodsinfo-container {
  width: 100%;
  padding: 5px;
  h3 {
    font-size: 16px;
    color: #225aff;
    text-align: center;
    margin: 15px 0;
  }
  .content {
    width: 100%;
    img{
      width: 100%;
    }
  }
}
</style>

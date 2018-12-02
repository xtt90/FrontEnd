<template>
  <div class="goods-list">
    <router-link class="goods-item" v-for="item in goodlist" :key="item.id" :to="'/home/goodsInfo/' + item.id" tag="div">
      <img :src='item.img_url' alt="">
      <h1 class="title">{{item.tilte}}</h1>
      <div class="info">
        <p class="price">
          <span class="now">¥ {{item.sell_price}}</span>
          <span class="old">¥ {{item.market_price}}</span>
        </p>
        <p class="sell">
          <span>热卖中</span>
          <span>剩{{item.isdel}}件</span>
        </p>
    </div>
    </router-link>

   <mt-button type="danger" size="large" @click="getMore">加载更多</mt-button>
    
  </div>
</template>

<script>
    export default{
      data(){
        return {
          pageindex:1,
          goodlist:[]

        }
      },
      created(){
        this.getGoodsList()
      },
      methods:{
        getGoodsList(){
          this.$http.get('api/getgoods?pageindex='+ this.pageindex).then(result=>{
              if(result.body.status===0){
                this.goodlist=this.goodlist.concat(result.body.message)
              }
          })
        },
        getMore(){
          this.pageindex++;
          this.getGoodsList()
        }
      
      }
    }
</script>

<style lang="less" scoped>

  .goods-list{
    display: flex;
    flex-wrap: wrap;
    padding: 7px;
    justify-content: space-between;

    .goods-item{
      width: 49%;
      text-align: center;
      margin: 4px 0;
      padding: 5px;
      border: 1px solid #ccc;
      box-shadow: 0 0 8px #ccc;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      min-height: 293px;
      img{
        margin-top: 15px;
        width: 100%;
      }
      .title {
        font-size: 14px;
      }

      .info{
        background-color: #eee;
        p {
          margin: 0;
          padding: 5px;
        }
      }
    
    .price{
      text-align: left;
      .now{
        color:red;
        font-size: 16px;
        font-weight: 700;
      }
      .old{
        margin-left: 15px;
        text-decoration: line-through;
        font-size: 12px;
      }
    }
    .sell{
      display: flex;
      justify-content: space-between;
      font-size: 13px;
    }
  }
}
</style>

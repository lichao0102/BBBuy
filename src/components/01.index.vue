<template>
    <div>
        <div class="section">
            <div class="location">
                <span>当前位置：</span>
                <a href="#/" class="router-link-active">首页</a> &gt;
                <a href="#/site/goodslist" class="router-link-exact-active router-link-active">购物商城</a>
            </div>
        </div>
        <div class="section">
            <div class="wrapper">
                <div class="wrap-box">
                    <div class="left-220" style="margin: 0px;">
                        <div class="banner-nav">
                            <ul>
                                <li v-for="(item) in catelist" :key="item.id">
                                    <h3>
                                        <i class="iconfont icon-arrow-right"></i>
                                        <span>{{item.title}}</span>
                                        <p>
                                            <span v-for="(itemSon) in item.subcates" :key="itemSon.id">
                                                {{itemSon.title}}&nbsp;
                                            </span>
                                        </p>
                                    </h3>
                                    <div class="item-box">
                                        <dl>
                                            <dt>
                                                <a href="/goods/40.html">{{item.title}}</a>
                                            </dt>
                                            <dd>
                                                <a v-for="(itemSon) in item.subcates" :key="itemSon.id" href="/goods/43.html">{{itemSon.title}}</a>
                                               
                                            </dd>
                                        </dl>
                                    </div>
                                </li>
                                
                            </ul>
                        </div>
                    </div>
                    <!--幻灯片-->
                    <div class="left-705">
                        <!-- <div class="banner-img">
                            <div id="focus-box" class="focus-box">
                                <ul class="slides">
                                    <li class="" style="width: 100%;height:100%; float: left; margin-right: -100%; position: relative; opacity: 0; display: block; z-index: 1;">
                                        <a href="/goods.html">
                                            <img style="width: 100%;height:100%;" src="http://39.108.135.214:8899/imgs/SJ4EgwosX0wTqvyAvhtFGT1w.jpg" draggable="false">
                                        </a>
                                    </li>
                                    <li style="width: 100%;height:100%; float: left; margin-right: -100%; position: relative; opacity: 1; display: block; z-index: 2;" class="flex-active-slide">
                                        <a href="/goods.html">
                                            <img style="width: 100%;height:100%;" src="http://39.108.135.214:8899/upload/201504/20/thumb_201504200314272543.jpg" draggable="false">
                                        </a>
                                    </li>
                                </ul>
                                <ol class="flex-control-nav flex-control-paging">
                                    <li>
                                        <a class="">1</a>
                                    </li>
                                    <li>
                                        <a class="flex-active">2</a>
                                    </li>
                                </ol>
                               
                            </div>

                        </div> -->
                          <el-carousel indicator-position="outside">
                                 <el-carousel-item v-for="(item) in sliderlist " :key="item.id">
                                    <img :src="item.img_url">
                                 </el-carousel-item>
                                </el-carousel>
                    </div>
                    <!--/幻灯片-->
                    <div class="left-220">
                        <ul class="side-img-list">
                            <li v-for="(item, index) in toplist" :key="item.id">
                                <div class="img-box">
                                    <label>{{index+1}}</label>
                                    <img :src="item.img_url">
                                </div>
                                <div class="txt-box">
                                    <a href="/goods/show-98.html">{{item.title}}</a>
                                    <span>{{item.add_time | filterData}}</span>
                                </div>
                            </li>
                          
                        </ul>
                    </div>
                </div>
            </div>
        </div>
        <div class="section" v-for="item in groupDate" :key="item.level1cateid">
            <div class="main-tit">
                <h2>{{item.catetitle}}</h2>
                <p>
                    <a href="/goods/43.html" v-for="itemSon1 in item.level2catelist" :key="itemSon1.subcateid">{{itemSon1.subcatetitle}}</a>
                    
                    <a href="/goods/40.html">更多
                        <i>+</i>
                    </a>
                </p>
            </div>
            <div class="wrapper clearfix">
                <div class="wrap-box">
                    <ul class="img-list">
                        <li v-for="itemSon2 in item.datas" :key="itemSon2.artID">
                           <router-link :to="'/detail/'+itemSon2.artID">
                                <div class="img-box">
                                    <img v-lazy="itemSon2.img_url">
                                </div>
                                <div class="info">
                                    <h3>{{itemSon2.artTitle}}</h3>
                                    <p class="price">
                                        <b>{{itemSon2.sell_price}}</b>元</p>
                                    <p>
                                        <strong>库存{{itemSon2.stock_quantity}}</strong>
                                        <span>市场价：
                                            <s>{{itemSon2.market_price}}</s>
                                        </span>
                                    </p>
                                </div>
                          </router-link>
                        </li>
                       
                    </ul>
                </div>
            </div>
        </div>
        
    </div>

</template>
<script>
    
    export default{
        name:"index",
        data:function(){
         return {
             catelist:[],
             sliderlist:[],
             toplist:[],
             groupDate:[]
         };
        }, 
        created() {
            this.$axios
            .get('site/goods/gettopdata/goods')
            .then((response)=>{
                
                  this.catelist=response.data.message.catelist
                  this.sliderlist=response.data.message.sliderlist
                  this.toplist=response.data.message.toplist
                //   console.log(this.catelist);
            //    console.log(response);
            })
                this.$axios
            .get('site/goods/getgoodsgroup')
            .then((response)=>{
                this.groupDate=response.data.message;
            })
        },
      
        // filters:{
        //     filterdata(val){
              
        //      }
        // }

    }
</script>

<style>
.el-carousel__item h3 {
    color: #475669;
    font-size: 18px;
    opacity: 0.75;
    /* line-height: 300px; */
    margin: 0;
  }
  
  .el-carousel__item:nth-child(2n) {
    background-color: #99a9bf;
  }
  
  .el-carousel__item:nth-child(2n+1) {
    background-color: #d3dce6;
  }
  .el-carousel__item{
      height: 326px;
  }
 .el-carousel__item img{
      width: 705px;
      height: 326px;
  }
  
</style>


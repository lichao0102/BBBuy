<template>

    <div>
        <div class="section">
            <div class="location">
                <span>当前位置：</span>
                <a href="/index.html">首页</a> &gt;
                <a href="/goods.html">购物商城</a> &gt;
                <a href="/goods/42/1.html">商品详情</a>
            </div>
        </div>
        <div class="section">
            <div class="wrapper clearfix">
                <div class="wrap-box">
                    <div class="left-925">
                        <div class="goods-box clearfix">
                            <div class="pic-box">
                            <ProductZoomer v-if="images.normal_size.length!=0" :base-images="images" :base-zoomer-options="zoomerOptions"></ProductZoomer>
                            </div>
                            <div class="goods-spec">
                                <h1>{{goodsinfo.title}}</h1>
                                <p class="subtitle">{{goodsinfo.sub_title}}</p>
                                <div class="spec-box">
                                    <dl>
                                        <dt>货号</dt>
                                        <dd id="commodityGoodsNo">{{goodsinfo.goods_no}}</dd>
                                    </dl>
                                    <dl>
                                        <dt>市场价</dt>
                                        <dd>
                                            <s id="commodityMarketPrice">¥{{goodsinfo.market_price}}</s>
                                        </dd>
                                    </dl>
                                    <dl>
                                        <dt>销售价</dt>
                                        <dd>
                                            <em id="commoditySellPrice" class="price">¥{{goodsinfo.sell_price}}</em>
                                        </dd>
                                    </dl>
                                </div>
                                <div class="spec-box">
                                    <dl>
                                        <dt>购买数量</dt>
                                        <dd>
                                            <div class="stock-box">
                                               <el-input-number v-model="buyCount" @change="buyCountChange" :min="0" :max="goodsinfo.stock_quantity" size="mini" label="描述文字"></el-input-number>
                                            </div>
                                            <span class="stock-txt">
                                                库存
                                                <em id="commodityStockNum">{{goodsinfo.stock_quantity}}</em>件
                                            </span>
                                        </dd>
                                    </dl>
                                    <dl>
                                        <dd>
                                            <div id="buyButton" class="btn-buy">
                                                <button onclick="cartAdd(this,'/',1,'/shopping.html');" class="buy">立即购买</button>
                                                <button @click="cartadd" class="add">加入购物车</button>
                                            </div>
                                        </dd>
                                    </dl>
                                </div>
                            </div>
                        </div>
                         
                           <div id="goodsTabs" class="goods-tab bg-wrap">
                               <Affix>
                            <div id="tabHead" class="tab-head" style="position: static; top: 517px; width: 925px;">
                                <ul>
                                    <li>
                                        <a href="javascript:;" @click="showDicuss=false" :class="{selected:!showDicuss}">商品介绍</a>
                                    </li>
                                    <li>
                                        <a href="javascript:;" @click="showDicuss=true" :class="{selected:showDicuss}">商品评论</a>
                                    </li>
                                </ul>
                            </div>
                             </Affix>
                            <div class="tab-content entry"  v-show="!showDicuss" v-html="goodsinfo.content">
                                内容
                            </div>
                            <div class="tab-content"  v-show="showDicuss">
                                <div class="comment-box">
                                    <div id="commentForm" name="commentForm"
                                        class="form-box">
                                        <div class="avatar-box">
                                            <i class="iconfont icon-user-full"></i>
                                        </div>
                                        <div class="conn-box">
                                            <div class="editor">
                                                <textarea id="txtContent" v-model.trim="commentInfo" name="txtContent" sucmsg=" " datatype="*10-1000" nullmsg="请填写评论内容！"></textarea>
                                                <span class="Validform_checktip"></span>
                                            </div>
                                            <div class="subcon">
                                                <input id="btnSubmit" name="submit" type="submit" value="提交评论" @click="submitCommit" class="submit">
                                                <span class="Validform_checktip"></span>
                                            </div>
                                        </div>
                                    </div>
                                    <ul id="commentList" class="list-box">
                                        <p v-show="comments.length==0" style="margin: 5px 0px 15px 69px; line-height: 42px; text-align: center; border: 1px solid rgb(247, 247, 247);">暂无评论，快来抢沙发吧！</p>
                                        <li v-for="item in comments" :key="item.id">
                                            <div class="avatar-box">
                                                <i class="iconfont icon-user-full"></i>
                                            </div>
                                            <div class="inner-box">
                                                <div class="info">
                                                    <span>{{item.user_name}}</span>
                                                    <span>{{item.reply_time | filterDate}} </span>
                                                </div>
                                                <p>{{item.content}}</p>
                                            </div>
                                        </li>
                                      
                                    </ul>
                                    <div class="page-box" style="margin: 5px 0px 0px 62px;">
                                        <!-- <div id="pagination" class="digg">
                                            <span class="disabled">« 上一页</span>
                                            <span class="current">1</span>
                                            <span class="disabled">下一页 »</span>
                                             
                                        </div> -->
                                         <Page :total="totalCount" show-elevator show-sizer placement="top" :page-size-opts="[5, 6,10, 13, 26]" @on-change="pageChange" @on-page-size-change="pageSizeChange" />
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="left-220">
                        <div class="bg-wrap nobg">
                            <div class="sidebar-box">
                                <h4>推荐商品</h4>
                                <ul class="side-img-list">
                                    <li v-for="item in hotgoodslist" :key="item.id">
                                        <div class="img-box">
                                            <router-link :to="'/detail/'+item.id">
                                                <img :src="item.img_url">
                                                </router-link>
                                           
                                        </div>
                                        <div class="txt-box">
                                            <router-link :to="'/detail/'+item.id"> {{item.title}}</router-link>
                                           
                                            <span>{{item.add_time | filterData}}</span>
                                        </div>
                                    </li>
                                 
                                </ul>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <BackTop :height="100" :bottom="200">
        <div class="top">返回顶端</div>
    </BackTop>
    <img v-if="imglist.length!=0" class="moveImg" style="display: none" :src="imglist[0].original_path" alt="">
    </div>

</template>
<script>
 import $ from 'jquery'


export default {
    name:"detail",
    data:function(){
        return {
            prductid:undefined,
            goodsinfo:{},//商品信息
            hotgoodslist:[],//热卖列表
            imglist:[],//图片列表
            buyCount:0,//购买数量
            showDicuss:false,// 是否显示评论 默认为false 默认显示 商品内容
            //  num1:0,
            zoomerOptions: {
           'zoomFactor': 5, // 放大倍数
           'pane': "container-round", // container-round 小放大镜
            'hoverDelay': 300,
            'namespace': "zoomer",
            'move_by_click': true, // true 点击切换
            'scroll_items': 7,
            'choosed_thumb_border_color': "yellowgreen" ,
            // 框的颜色
            },
            images:{
                normal_size:[

                ]
            },
            pageNum:1,
            pagesize:10,
            comments:[],
            totalCount:0,
            commentInfo:""
        }
    },
      methods:{
          buyCountChange(){
              console.log('变啦')
          },
          getproductDetail(){
        
           this.prductid=this.$route.params.id;
           
            this.$axios.get(`site/goods/getgoodsinfo/${this.prductid}`)
            .then((response)=>{
                this.goodsinfo=response.data.message.goodsinfo
               this.hotgoodslist=response.data.message.hotgoodslist
              this.imglist=response.data.message.imglist
               let temArr=[]

               this.imglist.forEach((v,i)=>{
                temArr.push({
                    id:v.id,
                    url:v.original_path
                })
                  })
               this.images.normal_size=temArr
               })
            },
         getComments(){
             this.$axios.get(`site/comment/getbypage/goods/${this.prductid}?pageIndex=${this.pageNum}&pageSize=${this.pagesize}`)
            .then((response)=>{
                        // console.log(response);
                        this.comments=response.data.message
                        this.totalCount=response.data.totalcount
             })
            },
          pageChange(page){
            //   console.log(page)
              this.pageNum=page
              this.getComments()
          }
          ,pageSizeChange(size){
            //   console.log(size)
               this.pagesize=size
               if(this.pageNum==1){
                   this.getComments()
               }
          },
          submitCommit(){
              if(this.commentInfo==""){
                  return this.$Message.error('不理你');
                  
              }
              this.$axios.post(`site/validate/comment/post/goods/${this.prductid}`,{
                  commenttxt:this.commentInfo,
                  
              }).then((response)=>{
                  this.$Message.success(response.data.message);
                  this.getComments();
                  this.commentInfo=""
              })
          },
          cartadd(){

              if(this.buyCount==0){
                  this.$Message.erroe('买点呗')
                  return
              }
              let cartOffset=$('.add').offset()

              let targetOffset=$('.icon-cart').offset()

              $('.moveImg').stop().show().addClass('move').css(cartOffset).animate(targetOffset,1000,function(){
                  $(this).hide().removeClass('move');
              }),
             //测试 增加数据
              this.$store.commit('addGoods',{
                  goodId:this.prductid,
                  goodNum:this.buyCount
              })
          }


      },
    beforeCreate() {
        console.log(this.$route)
    },
    created() {
    this.getproductDetail()
    this.getComments()
 },
 watch:{
     $route(val,oldval){
        //   console.log(val)
        //   console.log(oldval)
        this.images.normal_size=[]
         this.getproductDetail()
     }
 }
}
</script>
<style lang="less">
.tab-content img{
    width: 100%;
    display: block;
}
 .top{
        padding: 10px;
        background: rgba(0, 153, 229, .7);
        color: #fff;
        text-align: center;
        border-radius: 2px;
    }
    .pic-box{
        width: 395px;
    }
    .control-box .thumb-list{
        display: flex;
        justify-content: center;
        img{
            width: 80px;
            height: 80px;
            margin: 2px;
        }
        .control{
            display: flex;
            justify-content: center;
            align-items: center;
        }
    }
    .moveImg{
       position: absolute;
       width: 50px;
       height: 50px;
    //    display: none;
    }
    .moveImg.move{
        transition: transform  2s;
       transform: rotate(720deg)
    }

</style>




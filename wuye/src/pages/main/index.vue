<style scoped>
.wuye{font-family: PingFangSC-Regular;width: 100%;height: 800px;
      background-color:#ccc;font-size: 14px;text-align: center}
a{color: #000;opacity: 0.7;}
.ban1{width: 100%;}
.ban1 img{width: 100%;}
.jiugongge{width: 100%;height: 208px;background-color: white;}
.jgg_li{float: left;width: 33%;height: 104px; text-align: center;letter-spacing: 1.31px;font-size: 16px;font-family:PingFangSC-Regular;}
.jgg_img{margin: 15px auto 3px;}
.jgg_img img{width: 54px;}
.jgg-span{color: black;}
.inner{width: 100%;height: 350px;overflow: hidden; background-color: white;}
.inner1{width: 80%;height: 20px; margin:15px auto 15px;line-height: 20px;}
.spanl{font-size: 18px;letter-spacing: 1.38px;}
.spanr{font-size: 12px;letter-spacing: 1.12px;opacity: 0.5;color: #171717;padding-top: 3px;}
.title_li{width: 86%;height: 100px;overflow: hidden;margin: 0 auto;position: relative;}
/* .title_li div{float: left;} */
.title_img{width: 30%;height:86px;position: absolute;margin-left: 0;margin-top: 7px}
.title_img img{width: 100%;height:100%;margin:auto;}
.title_news{font-size: 14px; width: 70%;height: 85px; text-align: left;position: absolute;margin-left: 30%;margin-top:7px;}
.title_news span{padding: 0 20px;color: black;}
.xiaxian{height:1px;width:100%;background-color:#ccc; margin-top: 7px;}
p{padding: 0 20px;color: #565252;letter-spacing: 1.14px;overflow: hidden;
    display: -webkit-box;-webkit-line-clamp: 2;-webkit-box-orient: vertical;
    overflow: hidden;height: 34px;line-height: 17px;}
h6{text-align: right; padding: 0 15px;font-size: 11px;color:rgba(0,0,0,0.63);letter-spacing: 0.9px;}
</style>
<template>
    <div class="wuye">
        <swiper :options="swiperOption" ref="mySwiper">
            <swiper-slide>
                <div class="ban1">
                    <router-link to="/" >
                        <img src="../../assets/images/ysqban.png" alt="tt">
                    </router-link>                  
                </div> 
            </swiper-slide>
            <!-- <div class="swiper-pagination" slot="pagination"></div>        -->
        </swiper>
        
        <div class="jiugongge">
            <ul>
                <li class="jgg_li" >
                    <router-link to="/pay" class="link">
                        <div class="jgg_img">
                            <img src="../../assets/images/wyjf1.png" alt="tt">
                        </div>
                        <span class="jgg-span">物业缴费</span>
                    </router-link>
                </li>
                <li class="jgg_li" >    
                    <router-link to="/paystop" class="link">
                        <div class="jgg_img">
                            <img src="../../assets/images/tcjf1.png" alt="tt">
                        </div>
                        <span class="jgg-span">停车缴费</span>
                    </router-link>
                </li>
                <li class="jgg_li" >
                    <router-link to="/paymentquery" class="link">
                        <div class="jgg_img">
                            <img src="../../assets/images/jfcx1.png" alt="tt">
                        </div>
                        <span class="jgg-span">缴费查询</span>
                    </router-link>
                </li>
                <li class="jgg_li" >
                    <router-link to="/myhouse" class="link">
                        <div class="jgg_img">
                            <img src="../../assets/images/wsyz1.png" alt="tt">
                        </div>
                        <span class="jgg-span">我是业主</span>
                    </router-link>
                </li>
                <li class="jgg_li" >
                    <router-link :to="{path:'/suggest',query:{category:9}}" class="link">
                        <div class="jgg_img">
                            <img src="../../assets/images/yzyj1.png" alt="tt">
                        </div>
                        <span class="jgg-span">业主意见</span>
                    </router-link>
                </li>
                <li class="jgg_li" >
                    <div  class="link" @click="alert">
                        <div class="jgg_img">
                            <img src="../../assets/images/bmwx1.png" alt="tt">
                        </div>
                        <span class="jgg-span">便民维修</span>
                    </div>
                </li>
            </ul>
        </div> 

        <div style="width:100%;height:7px;"></div>
        <div class="inner">
          <div class="inner1">
            <span class="spanl fl"><strong>社区生活</strong></span>
            <span class="spanr fr">更多&gt;</span>
          </div>
          <ul class="title_ul"> 
            <li class="title_li" v-for="(news,index) in dataArr" :key="index">
              <div v-on:click="href(news.id)">
                <div class="title_img"> 
                  <img v-bind:src="news.smallImage" alt="">
                </div>
                <div class="title_news">
                  <p>{{news.summary}}</p>
                  <!-- <span>…</span> -->
                  <br>
                  
                  <h6 style="margin-top:10px;">生活百科</h6>
                </div>
                <div class="xiaxian"></div>
              </div>                        
            </li>
          </ul>
        </div>
        <div style="width:100%;height:80px;background:white;"></div> 
    </div>
</template>

<script>
let vm
import { MessageBox } from 'mint-ui';
import {swiper,swiperSlide} from 'vue-awesome-swiper'
export default {
    name: 'index',
    components: {
        swiper,
        swiperSlide
    },
    created(){
        vm = this;  
    },
    data () {
        return {
            dataArr:[],
            //swiper参数配置
            swiperOption:{
                notNextTick:true,
                autoplay:false,
                autoplay:{
                    disableOnInteraction:false,
                    // delay:20000000
                },
                pagination: {
                el: '.swiper-pagination'
                },
                loop: false,
            },
        };
    },

    computed: {},

    mounted(){
        // this.initSession4Test();
        this.initUserInfo();
    },

    methods: {
        //模仿线上用户信息/105/747/384/15184
        initSession4Test(){
            let url = '/initSession4Test/15184';
            vm.receiveData.getData(vm,url,'Data',function(){
                vm.initNews();
            });
        },

        initUserInfo(){
            let n = "GET",
                a = "userInfo",
                i = null,
                e = function(n) {
                    // console.log(JSON.stringify(n));
                    vm.initNews();
                },
                r = function() { 

                };
            vm.common.invokeApi(n, a, i, null, e, r);
        },
        initNews(){
            var page = 0;
            let n = "GET",
                a = "messages/"+page,
                i = null,
                e = function(n){
                    // console.log(JSON.stringify(n));
                    vm.dataArr = n.result;
                    page++;
                },
                r = function(){
                    
                };
            vm.common.invokeApi(n,a,i,null,e,r);
        },    
        href(mid){
            if(mid==15){
                window.location.href="http://mp.weixin.qq.com/s?__biz=MzA3Njk4ODgwMA==&mid=406333448&idx=1&sn=9b318dec9225d8fc1ce28b7a52007773#rd";
            }else if(mid==16){
                window.location.href="http://mp.weixin.qq.com/s?__biz=MzA3Njk4ODgwMA==&mid=407927486&idx=1&sn=c1f51214b1947b1b222af9a18e5593d6#rd";
            }else if(mid==17){
                window.location.href="http://mp.weixin.qq.com/s?__biz=MzA3Njk4ODgwMA==&mid=410063784&idx=1&sn=558b520c28f984ad7c0ed2a6ef692faf#rd";
            }else{
                this.$router.push({
                    path:'/news',
                        query:{
                            messageId:mid
                        }
                    })
            }
        },
        alert(){
            // 首页新闻
        
            MessageBox('该功能暂未开放','尽请期待!');
        }

    }
}

</script>
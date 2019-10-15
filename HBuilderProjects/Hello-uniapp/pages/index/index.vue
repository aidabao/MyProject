<template>
	<view>
	
		<!-- 轮播图 -->  
		<view class="part2">  
		    <swiper class="banner-box" indicator-dots autoplay  
		        indicator-active-color="#169bd5"  circular  
		        :interval="5000" :duration="300" indicator-color="rgba(0,0,0,.3)">  
		        <swiper-item v-for="(item, index) in bannerList" :key="index">  
		            <image class="banner-image" :src="item.img"  
		                mode="aspectFill" lazy-load></image>  
		        </swiper-item>  
		    </swiper>  
		</view>
		<view class="part3">
			<div class="row">
				<ul>
					<li v-for="(item,index) in part3Value" :key="index">
						<a :href="item.url">{{item.name}}</a>
					</li>
				</ul>
			</div>			
		</view>
		<view class="part4">
			<div class="row">
				<div class="col-sm-4" v-for="(item,index) in part4Value" :key="index">					
					<a :href="item.url">
						<image :src="item.img" style="width: 100%;"></image>
					</a>
				</div>
			</div>
		</view>
		<view class="part5">
		    <view class="page-body">
		        <view class="page-section page-section-gap" style="text-align: center;">
		            <audio style="text-align: left" :src="current.src" :poster="current.poster" :name="current.name" :author="current.author" :action="audioAction" controls></audio>
		        </view>
		    </view>
		</view>		
		<view class="part6">
		    <view>
		        <video id="myVideo" src="https://dcloud-img.oss-cn-hangzhou.aliyuncs.com/guide/uniapp/%E7%AC%AC1%E8%AE%B2%EF%BC%88uni-app%E4%BA%A7%E5%93%81%E4%BB%8B%E7%BB%8D%EF%BC%89-%20DCloud%E5%AE%98%E6%96%B9%E8%A7%86%E9%A2%91%E6%95%99%E7%A8%8B@20181126.mp4"
		            @error="videoErrorCallback" :danmu-list="danmuList" enable-danmu danmu-btn controls></video>
		    </view>
		    <!-- #ifndef MP-ALIPAY -->
		    <view class="uni-list uni-common-mt">
		        <view class="uni-list-cell">
		            <view>
		                <view class="uni-label">弹幕内容</view>
		            </view>
		            <view class="uni-list-cell-db">
		                <input v-model="danmuValue" class="uni-input" type="text" placeholder="在此处输入弹幕内容" />
		            </view>
		        </view>
		    </view>
		    <view class="uni-btn-v">
		        <button @click="sendDanmu" class="page-body-button">发送弹幕</button>
		    </view>
		            <!-- #endif -->
		</view>
	</view>
</template>

<script>
	export default {		
		data() {
			return {
				danmuValue:'',
				danmuList: [{
				                    text: '第 1s 出现的弹幕',
				                    color: '#ff0000',
				                    time: 1
				                },
				                {
				                    text: '第 3s 出现的弹幕',
				                    color: '#ff00ff',
				                    time: 3
				                }
				            ],
				title: '中国',
				count:1,
				bannerList:[
					{img:"http://bbsfiles.vivo.com.cn/vivobbs/attachment/forum/201807/15/211042gwc6e556yeqx6vqm.jpg"},
					{img:"http://img2.imgtn.bdimg.com/it/u=1300220885,2221741131&fm=26&gp=0.jpg"},
					{img:"http://img0.imgtn.bdimg.com/it/u=2204361223,656470001&fm=26&gp=0.jpg"}
				],
				part3Value:[
					{name:"限时秒杀",url:""},
					{name:"断码清仓",url:""},
					{name:"全球购",url:""},
					{name:"多多果园",url:""},
					{name:"9块9特卖",url:""},
					{name:"充值中心",url:""},
					{name:"百亿补贴",url:""},
					{name:"现金签到",url:""},
					{name:"金猪赚大钱",url:""},
					{name:"电器城",url:""}
				],
				part4Value:[
					{img:"https://m.360buyimg.com/babel/jfs/t1/44880/25/10765/73718/5d7c57ebEf1b46c62/c520848b35436a52.jpg.webp",url:"https://pro.jd.com/mall/active/g5ZY54ECKtaoYLkBvXcakpR7vCC/index.html"},
					{img:"https://img10.360buyimg.com/mobilecms/s140x140_jfs/t1/62081/19/8409/80829/5d64f9f3E7ce6a215/c32ca98235ed662e.jpg.webp",url:"https://miaosha.jd.com/#100007662658"},
					{img:"https://img20.360buyimg.com/mobilecms/s140x140_jfs/t1/52611/10/10282/104384/5d773ad1Eb3ad13ed/084027e01ca1ce79.jpg.webp",url:"https://item.jd.com/30760231260.html"},
					{img:"https://img13.360buyimg.com/mobilecms/s140x140_jfs/t1/7484/14/11814/294483/5c305c45Ef8b46a67/4492491116c52f44.jpg.webp",url:"https://item.jd.com/30760231260.html"},
					{img:"https://img20.360buyimg.com/mobilecms/s140x140_jfs/t1/44488/39/9518/203902/5d6e2397E574928a8/7b20c982fd1c7994.jpg.webp",url:"https://item.jd.com/30760231260.html"},
					{img:"https://img20.360buyimg.com/mobilecms/s140x140_jfs/t1/57871/1/10518/88708/5d7a0138Eb641ef85/76896b115790da2e.jpg.webp",url:"https://item.jd.com/30760231260.html"}
				],
				current: {
				                poster: 'https://img-cdn-qiniu.dcloud.net.cn/uniapp/audio/music.jpg',
				                name: '致爱丽丝',
				                author: '暂无',
				                src: 'https://img-cdn-qiniu.dcloud.net.cn/uniapp/audio/music.mp3',
				            },
				audioAction: {
				    method: 'pause'
				}
			}
		},
		onLoad() {	
		},
		methods: {	
			onReady: function(res) {
			    // #ifndef MP-ALIPAY
			    this.videoContext = uni.createVideoContext('myVideo')
			    // #endif
			},
			test:function(){
				uni.showModal({
				    title: '提示',
				    content: '这是一个模态弹窗',
				    success: function (res) {
				        if (res.confirm) {
				            console.log('用户点击确定');
				        } else if (res.cancel) {
				            console.log('用户点击取消');
				        }
				    }
				});
			},
			sendDanmu: function() {
			    this.videoContext.sendDanmu({
			        text: this.danmuValue,
			        color: this.getRandomColor()
			    });
			    this.danmuValue = '';
			},
			videoErrorCallback: function(e) {
			    uni.showModal({
			        content: e.target.errMsg,
			        showCancel: false
			    })
			},
			getRandomColor: function() {
			    const rgb = []
			        for (let i = 0; i < 3; ++i) {
			            let color = Math.floor(Math.random() * 256).toString(16)
			            color = color.length == 1 ? '0' + color : color
			            rgb.push(color)
			        }
			        return '#' + rgb.join('')
			}

		}
	}
	
</script>

<style>
	@import url("https://cdn.jsdelivr.net/npm/bootstrap@3.3.7/dist/css/bootstrap.min.css");
	.nav{
		padding-left: 10px;
		text-underline: none;
		color: #4CD964;
	}
	/* 轮播图 */  
	.part2{  
	    width: 100%;  
	    height: 260px;  
	    border-bottom: 20px solid #f9f9f9;  
	    overflow: hidden;  
	    position: relative;  
	}  
	.part2:after{  
	    content: " ";  
	    height: 20px;  
	    border-radius: 50%;  
	    background: #f9f9f9;  
	    position: absolute;  
	    bottom: -10px;  
	    left: -20px;  
	    right: -20px;  
	}  
	.banner-box{  
	    width: 100%;  
	    height: 100%;  
	}  
	.banner-image{  
	    width: 100%;  
	    height: 100%;  
	}
	.part3 ul{
		padding: 0;
		margin: 0;
	}
	.part3 li{
		list-style: none;
		float: left;
		padding-left: 5px;
	}
	.part3 li a{
		text-decoration: none;
		color: #808080;
	}
</style>

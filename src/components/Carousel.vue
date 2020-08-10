<template>
  <div>
      <div class="carousel" :style="{'width':width,'height':height}">
          <div class="wrapper">
              <img  v-for="(item,i) in imgData " :key="i" :src="item.url"
                :style="{'width':width,'height':height}"
               v-show="i==index" @click="linkTo(item.link)"/>
          </div>
      </div>
      <div class="banner" :style="{'width':width}">
          <span v-for="(item,i) in banners" :class="{'curIndx':i==index}"
          @click="changeIndex(i)" :key="i">
          </span>
      </div>
  </div>
</template>

<script>

//跑马灯组件

export default {
    props:{
        imgData:{
            type:Array,
            default:()=>[]
        },
        timeSpan:{
            type:Number,
            default:2000
        },
        width:{
            type:String,
            default:'300px'
        },
        height:{
            type:String,
            default:'150px'
        },
    },
    data:function(){
        return {
            timer:null,
            index:0
        }
    },
    methods:{
        nexts() {
            this.index++;
            var val=this.imgData.length;
            if (this.index > --val) {
                this.index = 0;
            };
        },
        autoPlay() {
            var that=this;
            this.timer = setInterval(function() {
                that.nexts();
            }, this.timeSpan)
        },
        changeIndex(i){
            this.index=i;
        },
        linkTo(url){
            console.log(url);
            this.$router.push({path:url});
        }
    },
    computed:{
        banners(){
            var banners=[];
            var lenths=this.imgData.length;
            for(var i=1;i<lenths+1;i++){
                banners.push(i);
            }
            return banners;
        }
    },
    mounted(){
        this.autoPlay();
    },
    destroyed(){
        this.timer=null;
    }
}
</script>

<style  scoped>
    .carousel {
        position:relative;
        overflow: hidden;
    }
    .wrapper{
        position: absolute;
        width:1200px;
        overflow: hidden;
        height:150px;
    }
    .wrapper img {
        float: left;
        left:0;
    }

    .banner{
        margin:30px auto;
        text-align: center;
        
    }
        .banner span{
            width:10px;
            height:10px;
            border-radius:50%;
            background:#eee;
            display: inline-block;
            margin:0 10px;
            line-height: 10px;
        }
        .banner .curIndx{
            background:red;
        }
</style>
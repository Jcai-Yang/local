<template>
  <div class="photoinfo-container">
    <h3>{{ photoinfo.title }}</h3>
    <p class="subtitle">
    <!--
      <span>发表时间：{{ photoinfo.add_time | dateFormat }}</span>
    -->
     <span>发表时间：2019-09-09 14:31:02</span>
      <span>点击：{{ photoinfo.click }}次</span>
    </p>

    <hr>

    <!-- 缩略图区域 -->
    <div class="thumbs">
      <img class="preview-img" v-for="(item, index) in list" :src="item.src" height="100" @click="$preview.open(index, list)" :key="item.src">
    </div>

    <!-- 图片内容区域 -->
    <div class="content" v-html="photoinfo.content"></div>

    <!-- 放置一个现成的 评论子组件 -->
    <cmt-box :id="id"></cmt-box>
  </div>
</template>

<script>
// 1. 导入评论子组件
import comment from "../subcomponents/comment.vue";
import getimageInfojson from "../../json/getimageInfo.json";
import getthumimagesjson from "../../json/getthumimages.json";

export default {
  data() {
    return {
      id: this.$route.params.id, // 从路由中获取到的 图片Id
      photoinfo: {}, // 图片详情
      list: [] // 缩略图的数组
    };
  },
  created() {
    this.getPhotoInfo();
    this.getThumbs();
  },
  methods: {
    getPhotoInfo() {
      // 获取图片的详情
        if (getimageInfojson.status === 0) {
          this.photoinfo = getimageInfojson.message[0];
        }
    },
    getThumbs() {
      // 获取缩略图
        if (getthumimagesjson.status === 0) {
          // 循环每个图片数据，补全图片的宽和高
          getthumimagesjson.message.forEach(item => {
            item.w = 600;
            item.h = 400;
          });
          // 把完整的数据保存到 list 中
          console.log(getthumimagesjson.message[0])
          this.list = getthumimagesjson.message;
        }
    }
  },
  components: {
    // 注册 评论子组件
    "cmt-box": comment
  }
};
</script>

<style lang="scss" scoped>
.photoinfo-container {
  padding: 3px;
  h3 {
    color: #26a2ff;
    font-size: 15px;
    text-align: center;
    margin: 15px 0;
  }
  .subtitle {
    display: flex;
    justify-content: space-between;
    font-size: 13px;
  }

  .content {
    font-size: 13px;
    line-height: 30px;
  }

  .thumbs{
    img{
      margin: 10px;
      box-shadow: 0 0 8px #999;
    }
  }
}
</style>

<template>
  <div class="cmt-container">
    <h3>发表评论</h3>
    <hr>
    <textarea placeholder="请输入要评论的内容（做多评论20字）" maxlength="120" v-model="content"></textarea>

    <mt-button type="primary" size="large"   @click="postComment">发表评论</mt-button>

    <div class="cmt-list">
      <div class="cmt-item" v-for="(item, i) in comments" :key="item.add_time">
        <div class="cmt-title">
          用户：{{ item.user_name }}&nbsp;&nbsp;发表时间：{{ item.add_time | dateFormat }}
        </div>
        <div class="cmt-body">
          {{ item.content === 'undefined' ? '此用户很懒，嘛都没说': item.content }}
        </div>
      </div>

    </div>

    <mt-button type="danger" size="large" plain >加载更多</mt-button>
  </div>
</template>

<script>
import { Toast } from "mint-ui";
export default {
  data() {
    return {
    	comments: [], // 所有的评论数据
      content: "", // 默认展示第一页数据
      user_name: "匿名用户" // 评论输入的内容
    };
  },
  created() {
    this.getComments();
  },
  methods: {
    getComments() {
      var list = JSON.parse(localStorage.getItem('cmts') || '[]')
          this.comments = list
    },
    postComment() {
      // 校验是否为空内容
      if (this.content.trim().length === 0) {
        return Toast("评论内容不能为空！");
      }

			var comment = { add_time: Date.now(), user_name: this.user_name, content: this.content }
   		var list = JSON.parse(localStorage.getItem('cmts') || '[]')
      list.unshift(comment)
      localStorage.setItem('cmts', JSON.stringify(list))
			this.content = ''
       this.getComments()
    }
  },
  props: ["id"]
};
</script>

<style lang="scss" scoped>
.cmt-container {
  h3 {
    font-size: 18px;
  }
  textarea {
    font-size: 14px;
    height: 85px;
    margin: 0;
  }

  .cmt-list {
    margin: 5px 0;
    .cmt-item {
      font-size: 13px;
      .cmt-title {
        line-height: 30px;
        background-color: #ccc;
      }
      .cmt-body {
        line-height: 35px;
        text-indent: 2em;
      }
    }
  }
}
</style>

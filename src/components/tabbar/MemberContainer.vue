<template>
  <div class="member-container">
  <!-- 上面部分 -->
   <div class="first-con">
   <div class="first-item">
      <div class="title">头像</div>
      <div class="content">
      <img  src="../../images/ml3.jpg"/>
      </div>
    </div>
    <div class="first-item">
      <div class="title">姓名</div>
      <div class="content">猫和老鼠</div>
    </div>
    <div class="first-item">
      <div class="title">账号</div>
      <div class="content">Jerry@dcloud.io</div>
    </div>
   </div>
   

   <!-- 下面部分 -->
   <div class="second-con">
    <div class="second-item">
      <div class="title">QQ号</div>
      <div class="content">88888888</div>
    </div>
    <div class="second-item">
      <div class="title">手机号</div>
      <div class="content">12345678900</div>
    </div>
    <div class="second-item">
      <div class="title">邮箱地址</div>
      <div class="content">Jerry@dcloud.io</div>
    </div>
   </div>

  </div>
</template>

<script>
</script>

<style lang="scss" scoped>
.member-container{
  background-color: #eee;
  overflow: hidden;
  .first-con{
    border: 1px solid #eee;
    margin: 10px 0;
    background: white;
   .first-item{
     display: flex;
     align-items: center;
    justify-content: space-between;
    padding: 15px;
    border-bottom: 1px solid #eee;
    background:white;
    .content{
      display:flex;
      justify-content:space-between;
      align-items:center;
    img{
      height:50px;
      width:50px;
      border-radius:50%;
      margin-right:10px;
    }
    }
   }
  }
  .second-con{
    background: white;
    border: 1px solid #eee;
    margin: 10px 0;
   .second-item{
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px;
    border-bottom: 1px solid #eee;
    background:white;
  }
  }

}
</style>

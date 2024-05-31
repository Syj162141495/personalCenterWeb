<template>
  <div class="background4">
    <div class="module_title">医保卡结算</div>
    <div class="card">
      <div class="card-number">卡号:1234567</div>
      <div class="card-numbers">
        <div class="card-number-left">
          <div class="align-items-center">
            <div>本年度医疗消费</div>
            <div class="flex ml-6">
              <div class="d-inline insurance-number-size">1000</div>
              <div class="d-inline yuan-size">元</div>
            </div>
          </div>
        </div>
        <div class="card-number-right">
          <div>本年度医保结算</div>
          <div class="flex ml-12">
            <div class="d-inline insurance-number-size2">900</div>
            <div class="d-inline yuan-size">元</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script lang="ts" setup></script>
<style>
  .background4 {
    /* height: 75%; */
    background-color: #ffffff;
    border-radius: 10px; /* 圆角半径 */
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2); /* 阴影样式 */
  }

  .card {
    border-radius: 10px;
    border: #aaa solid 2px;
    padding: 0px;
    margin-left: 200px;
    margin-right: 200px;
    margin-top: 10px;
    margin-bottom: 10px;
    height: 80%;
    background-color: #96c0dc97;
  }

  .card-number {
    position: absolute;
    left: 0.1;
    bottom: 1;
    background-color: #aaa;
    color: #fff;
    padding: 8px;
    border-radius: 10px 0 0 0;
  }

  .card-numbers {
    display: flex;
    justify-content: center;
    margin-top: 60px;
    font-size: 20px;
  }

  .card-number-left {
    text-align: center;
  }
  .card-number-right {
    margin-left: 100px;
    text-align: center;
  }

  .insurance-number-size {
    font-size: larger;
    color: #005d7f;
  }

  .insurance-number-size2 {
    font-size: larger;
    color: #3f7a60;
  }

  .yuan_size {
    /* font-size: small; */
    font-size: 10px;
  }
</style>

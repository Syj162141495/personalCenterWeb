<template>
  <div class="background1">
    <div class="module_title">基本信息</div>
    <div class="md:flex enter-y basic-content">
      <div class="md:w-1/10"></div>
      <div class="md:w-9/10">
        <div class="first-line flex">
          <div class="d-inline flex">
            <div class="d-inline mr-2 item_title">姓名</div>
            <div class="d-inline mr-2 content-title"> {{ propleInfo.patientName }}</div>
          </div>
          <div class="d-inline flex">
            <div class="d-inline mr-2 item_title">性别</div>
            <div class="d-inline mr-2 content-title">{{ propleInfo.sex == '1' ? '男' : '女' }}</div>
          </div>
          <div class="d-inline flex">
            <div class="d-inline mr-2 item_title">年龄</div>
            <div class="d-inline mr-2 content-title">{{ propleInfo.age || '---' }}</div>
          </div>
          <div class="d-inline flex">
            <div class="d-inline ml-90 item_title">病症</div>
            <div class="d-inline ml-2 mr-2 content-title">{{ propleInfo.illness || '---' }}</div>
          </div>
        </div>
        <div class="hr-style"></div>
        <div class="second-line flex">
          <div class="d-inline flex">
            <div class="d-inline mr-2 item_title">身高</div>
            <div class="d-inline mr-2 content-title">{{ propleInfo.height || '---' }}cm</div>
          </div>
          <div class="d-inline flex">
            <div class="d-inline mr-2 item_title">体重</div>
            <div class="d-inline mr-2 content-title">{{ targetProperty || '---' }}kg</div>
          </div>
          <div class="d-inline flex">
            <div class="d-inline mr-2 item_title">BMI</div>
            <div class="d-inline mr-2 content-title">{{ bmidata?.toFixed(2) || '---' }}</div>
          </div>
        </div>
        <div class="hr-style"></div>
        <div class="third-line"></div>
      </div>
    </div>
    <div class="align-right d-inline flex mr-20 mt-15">
      <button @click="eventclick" class="tip-style">完善个人信息</button>
      <Icon @click="eventclick" icon="open-left|svg" class="mt-3 ml-2" size="23" />
    </div>
    <InputForm @register="registerDrawer" />
  </div>
</template>
<script lang="ts" setup>
  import { propleInfo, targetProperty } from './info-utils';
  import InputForm from '/@/views/information/basicInformation/form.vue';
  import { useDrawer } from '/@/components/Drawer';
  import { Icon } from '/@/components/Icon';
  const [registerDrawer, { openDrawer }] = useDrawer();

  function eventclick() {
    openDrawer(true, { id: propleInfo.id });
  }
  function calculateBMI(): number | undefined {
    if (propleInfo.height && targetProperty) {
      const heightInMeters = propleInfo.height / 100; // 将身高从厘米转换为米
      const bmi = targetProperty / (heightInMeters * heightInMeters);
      return bmi;
    }
  }

  const bmidata = calculateBMI();
</script>
<style>
  .background1 {
    /* background-color: #abbaea; */
    background-color: white;
    border-radius: 10px; /* 圆角半径 */
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.2); /* 阴影样式 */
  }
  .basic-content {
    margin-top: 20px;
  }

  .hr-style {
    border-top: 2px solid #48a9ee;
    margin-right: 10%;
  }

  .module_title {
    color: #000000;
    font-size: large;
    margin-left: 10px;
    font-family: 'Microsoft YaHei', 微软雅黑;
  }

  .item_title {
    font-weight: bold;
    font-size: small;
    font-family: 'Microsoft YaHei', 微软雅黑;
    margin-top: 10px;
    color: #5e8599;
  }

  .content-title {
    color: #000000;
    font-size: large;
    font-family: 'Microsoft YaHei', 微软雅黑;
    margin-bottom: 5px;
    margin-top: 5px;
    margin-right: 20px;
  }
  .align-right {
    justify-content: flex-end;
  }

  .tip-style {
    font-weight: bold;
    font-size: medium;
    font-family: 'Microsoft YaHei', 微软雅黑;
    margin-top: 10px;
    color: #5e8599;
  }
</style>

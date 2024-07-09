<template>
  <div>
    <div class="md:flex">
      <div class="enter-y md:w-1/2">
        <Search class="md:mb-2" />
        <SiteAnalysis class="enter-y mt-2" />
        <div class="mt-2">
          <NowInfo class="w-full" />
          <Report class="w-full mt-2" />
          <MyReserve class="w-full mt-2" />
        </div>
      </div>
      <div class="enter-y md:w-1/2">
        <BasicInfo class="w-full !md:mx-4 !md:my-0 h-2/8" />
        <HealthEvent class="w-full !my-4 !md:mx-4 md:h-3/7" />
        <MedicalInsurance class="w-full !md:mx-4 h-2/8" :propleInfo="userInfo" />
      </div>
    </div>
  </div>
</template>
<script lang="ts" setup name="Analysis">
  import NowInfo from './components/NowInfo.vue';
  import Report from './components/Report.vue';
  import Search from './components/Search.vue';
  import MyReserve from './components/MyReserve.vue';
  import GrowCard from './components/GrowCard.vue';
  import SiteAnalysis from './components/SiteAnalysis.vue';
  import VisitSource from './components/VisitSource.vue';
  import VisitRadar from './components/VisitRadar.vue';
  import SalesProductPie from './components/SalesProductPie.vue';
  import BasicInfo from './components/BasicInfo.vue';
  import HealthEvent from './components/HealthEvent.vue';
  import MedicalInsurance from './components/MedicalInsurance.vue';
  import { ref, onMounted } from 'vue';
  import { getBaseInfo } from '/@/api/sys/desktopApi';
  import { useUserStore } from '/@/store/modules/user';
  const userStore = useUserStore();
  console.log(userStore);
  // 使用 ref 创建一个响应式引用
  const userInfo = ref({});
  // const phone = userStore?.patientPhone ?? '13021646422';
  const phone = (userStore as { patientPhone?: string }).patientPhone ?? '13021646422';
  // const phone = '13021646422';
  onMounted(async () => {
    try {
      // 调用异步函数并等待结果
      const data = await getBaseInfo({
        phone: phone,
      });
      console.log(data);
      // 更新响应式引用
      userInfo.value = data;
      // 处理从 getBaseInfo 返回的数据
      // console.log(data);
    } catch (error) {
      // 处理从 getBaseInfo 抛出的错误
      console.error(error);
    }
  });
</script>

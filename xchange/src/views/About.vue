<template>
  <div class="about">
    <HistoricalData
      warning="Historical Data only applies to dates after January 1st, 2000"
    />
  </div>
</template>

<script>
import HistoricalData from "@/components/HistoricalData.vue";

export default {
  components: {
    HistoricalData,
  },
  // data() {
  //   return {
  //     warning: "Historical Data only applies to dates after January 1st, 2000",
  //   };
  // },
};
</script>

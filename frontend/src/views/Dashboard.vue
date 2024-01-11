<template>
  <div class="content">
    <b-row>
      <b-col cols="8">
        <h2>Trending Event</h2>
      </b-col>
      <b-col cols="4">
        <h3>Total Pendapatan</h3>
      </b-col>
    </b-row>
    <b-row>
      <b-col cols="8">
        <Trending />
      </b-col>
      <b-col cols="4">
        <br />
        <RevenueReport />
      </b-col>
    </b-row>
    <b-row>
      <b-col cols="12">
        <h2>Semua Event</h2>
      </b-col>
    </b-row>
    <b-row>
      <b-col cols="12">
        <AllCards />
      </b-col>
    </b-row>
    <!-- <b-row>
      <b-col cols="12">
        <h2>Informal</h2>
      </b-col>
    </b-row>
    <b-row>
      <b-col cols="12">
        <FunCards />
      </b-col>
    </b-row> -->
  </div>
</template>

<script>
import Trending from '@/components/Trending.vue';
import RevenueReport from '@/components/RevenueReport.vue';
import AllCards from '@/components/AllCards.vue';
// import FunCards from '@/components/FunCards.vue';

export default {
  components: {
    Trending,
    RevenueReport,
    AllCards,
    // FunCards,
  },
};
</script>

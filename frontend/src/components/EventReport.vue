<template>
  <div class="center">
    <vs-table striped class="report-table">
      <template #thead>
        <vs-tr>
          <vs-th>Event ID</vs-th>
          <vs-th>Nama</vs-th>
          <vs-th>Penyelenggara</vs-th>
          <vs-th>Tanggal</vs-th>
          <vs-th>Tipe Tiket</vs-th>
          <vs-th>Harga Normal</vs-th>
          <vs-th>Harga Silver</vs-th>
          <vs-th>Harga Gold</vs-th>
          <vs-th>Harga Platinum</vs-th>
          <vs-th>Total Pendapatan</vs-th>
        </vs-tr>
      </template>
      <template #tbody>
        <vs-tr :key="i" v-for="(tr, i) in report_data" :data="tr">
          <vs-td>#{{ tr.event_id }}</vs-td>
          <vs-td>{{ tr.e_name }}</vs-td>
          <vs-td>{{ tr.e_organizer }}</vs-td>
          <vs-td>{{ tr.e_date }}</vs-td>
          <vs-td v-if="tr.t_type == 0">Normal</vs-td>
          <vs-td v-if="tr.t_type == 1">Premium</vs-td>
          <vs-td>Rp.{{ tr.n_rev }}</vs-td>
          <vs-td>Rp.{{ tr.s_rev }}</vs-td>
          <vs-td>Rp.{{ tr.g_rev }}</vs-td>
          <vs-td>Rp.{{ tr.p_rev }}</vs-td>
          <vs-td>Rp.{{ tr.total_revenue }}</vs-td>
        </vs-tr>
      </template>
    </vs-table>
  </div>
</template>

<script>
import axios from '../vuexios';

export default {
  data() {
    return {
      report_data: [],
    };
  },
  mounted() {
    axios
      .get('/getsalesdetails')
      .then(response => {
        this.report_data = response.data;
      })
      .catch(error => console.log(error.message));
  },
  name: 'EventReport',
};
</script>

<style scoped>
.report-table {
  height: 500px !important;
  overflow: auto;
}
</style>

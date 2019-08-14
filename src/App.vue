<template>
  <div id="app">
    <h1>Arts for wall control panel</h1>
    <el-tabs type="border-card">
      <el-tab-pane>
        <span slot="label"><i class="el-icon-date"></i> Current orders</span>
        <CustomersTable :ordersData="currentOrders"/>
      </el-tab-pane>
      <el-tab-pane>
        <span slot="label"><i class="el-icon-s-order"></i> Completed orders</span>
        <CustomersTable :ordersData="completedOrders"/>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
import CustomersTable from './components/CustomersTable.vue'

export default {
  name: 'app',
  data() {
    return {
        completedOrders: [
            {
                date_added: '2019-08-08 06:59:05',
                customer_id: '1474',
                customer_name: 'John Doe',
                poster_variable: 'POSTER CODE: 39282 POSTER TYPE: Print POSTER SIZE: A4',
                poster_preview: 'click to preview poster',
                generate_poster: 'generate',
                download_file: 'generate',
                send_to_customer: 'generate',
                mark_complete: 'generate'

            },
            {
                date_added: '2019-08-08 06:59:05',
                customer_id: '1474',
                customer_name: 'John Doe',
                poster_variable: 'POSTER CODE: 39282 POSTER TYPE: Print POSTER SIZE: A4',
                poster_preview: 'click to preview poster',
                generate_poster: 'generate',
                download_file: 'generate',
                send_to_customer: 'generate',
                mark_complete: 'generate'

            }
        ],
        currentOrders: [
        {
          date_added: '2019-08-08 06:44:07',
          customer_id: '1473',
          customer_name: 'Shaik',
          poster_variable: 'POSTER CODE: 34799 POSTER TYPE: Framed POSTER SIZE: 28inX40in',
          poster_preview: 'http://3a2.7a4.myftpupload.com/product/star-poster/?updateposter=34799',
          generate_poster: 'generate',
          download_file: 'generate',
          send_to_customer: 'generate',
          mark_complete: 'generate'
        },
        {
            date_added: '2019-08-08 06:59:05',
            customer_id: '1474',
            customer_name: 'John Doe',
            poster_variable: 'POSTER CODE: 39282 POSTER TYPE: Print POSTER SIZE: A4',
            poster_preview: 'click to preview poster',
            generate_poster: 'generate',
            download_file: 'generate',
            send_to_customer: 'generate',
            mark_complete: 'generate'

        }
       ]
    }
  },
  components: {
    CustomersTable
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

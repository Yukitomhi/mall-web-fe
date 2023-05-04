<template> 
  <div class="app-container">
    <el-card class="operate-container" shadow="never">
      <i class="el-icon-tickets"></i>
      <span>Shipping list</span>
    </el-card>
    <div class="table-container">
      <el-table ref="deliverOrderTable"
                style="width: 100%;"
                :data="list" border>
        <el-table-column label="Order number" width="180" align="center">
          <template slot-scope="scope">{{scope.row.orderSn}}</template>
        </el-table-column>
        <el-table-column label="Recipient" width="180" align="center">
          <template slot-scope="scope">{{scope.row.receiverName}}</template>
        </el-table-column>
        <el-table-column label="Phone number" width="160" align="center">
          <template slot-scope="scope">{{scope.row.receiverPhone}}</template>
        </el-table-column>
        <el-table-column label="Postal code" width="160" align="center">
          <template slot-scope="scope">{{scope.row.receiverPostCode}}</template>
        </el-table-column>
        <el-table-column label="Shipping address" align="center">
          Dongxiao Subdistrict, Futian District, Shenzhen City, Guangdong Province
          <!--<template slot-scope="scope">{{scope.row.address}}</template>-->
        </el-table-column>
        <el-table-column label="Shipping method" width="160" align="center">
          <template slot-scope="scope">
            <el-select
                       v-model="scope.row.deliveryCompany"
                       size="small">
              <el-option v-for="item in companyOptions"
                         :key="item"
                         :label="item"
                         :value="item">
              </el-option>
            </el-select>
          </template>
        </el-table-column>
        <el-table-column label="Shipping number" width="180" align="center">
          <template slot-scope="scope">
            <el-input size="small" v-model="scope.row.deliverySn"></el-input>
          </template>
        </el-table-column>
      </el-table>
      <div style="margin-top: 15px;text-align: center">
        <el-button @click="cancel">Cancel</el-button>
        <el-button @click="confirm" type="primary">Confirm</el-button>
      </div>
    </div>
  </div>
</template>
<script>
  import {deliveryOrder} from '@/api/order'
  const defaultLogisticsCompanies=["SF Express", "YTO Express", "ZTO Express", "Yunda Express"];
  export default {
    name: 'deliverOrderList',
    data() {
      return {
        list:[],
        companyOptions:defaultLogisticsCompanies
      }
    },
    created(){
      this.list= this.$route.query.list;
      //当list不为数组时转换为数组
      if(this.list instanceof Array===false){
        this.list=[];
      }
    },
    methods:{
      cancel(){
        this.$router.back();
      },
      confirm(){
        this.$confirm('Are you sure you want to perform this operation?', 'Tip', {
          confirmButtonText: 'Confirm',
          cancelButtonText: 'Cancel',
          type: 'warning'
        }).then(() => {
          deliveryOrder(this.list).then(response=>{
            this.$router.back();
            this.$message({
              type: 'success',
              message: 'Successful!'
            });
          });
        }).catch(() => {
          this.$message({
            type: 'info',
            message: 'Cancel'
          });
        });
      }
    }
  }
</script>
<style></style>



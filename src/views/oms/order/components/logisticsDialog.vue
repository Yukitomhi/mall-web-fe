<template> 
  <el-dialog title="Tracking"
             :visible.sync="visible"
             :before-close="handleClose"
             width="40%">
    <el-steps direction="vertical"
              :active="6"
              finish-status="success"
              space="50px">
      <el-step  v-for="item in logisticsList"
                :key="item.name"
                :title="item.name"
                :description="item.time"></el-step>
    </el-steps>
  </el-dialog>
</template>
<script>
  const defaultLogisticsList=[
    {name: 'Order submitted, waiting for payment',time:'2017-04-01 12:00:00 '},
    {name: 'Order payment successful',time:'2017-04-01 12:00:00 '},
    {name: 'Scan in the lower-level location in Beijing, waiting for payment',time:'2017-04-01 12:00:00 '},
    {name: 'Unload scan in the Guangdong Shenzhen company, waiting for payment',time:'2017-04-01 12:00:00 '},
    {name: 'Send-out scan in the Guangdong Shenzhen company',time:'2017-04-01 12:00:00 '},
    {name: 'Arrive at the destination network node in Guangdong Shenzhen company, the express will be delivered soon',time:'2017-04-01 12:00:00 '},
    {name: 'Order signed, looking forward to serving you again',time:'2017-04-01 12:00:00 '}
  ];
  export default {
    name:'logisticsDialog',
    props: {
      value: Boolean
    },
    computed:{
      visible: {
        get() {
          return this.value;
        },
        set(visible){
          this.value=visible;
        }
      }
    },
    data() {
      return {
        logisticsList:Object.assign({},defaultLogisticsList)
      }
    },
    methods:{
      emitInput(val) {
        this.$emit('input', val)
      },
      handleClose(){
        this.emitInput(false);
      }
    }
  }
</script>
<style></style>



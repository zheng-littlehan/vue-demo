<template>
  <div>
    <this-dialog :is-show="isShowCheckDialog" @on-close="checkStatus()">
      <img src="../assets/logo.png"/>
      请检查你的支付状态！
      <div class="button" @click="checkStatus()">
        支付成功
      </div>
      <div class="button" @click="checkStatus()">
        支付失败
      </div>
    </this-dialog>
    <this-dialog :is-show="isShowSuccessDialog"  @on-close="closeSuc()">
      购买成功！
    </this-dialog>
    <this-dialog :is-show="isShowFailDialog" @on-close="closeFail()">
      购买失败！
    </this-dialog>
  </div>
</template>

<script>
  import Dialog from './dialog'

  export default {
    components: {
      thisDialog: Dialog
    },
    props: {
      isShowCheckDialog:{
        type:Boolean,
        default:false,
      },
      orderId: {
        type: [String, Number]
      }
    },
    data() {
      return {
        isShowSuccessDialog: false,
        isShowFailDialog: false
      }
    },
    methods: {
      checkStatus() {
        this.$http.post('/api/corder', {orderId: this.orderId}).then(
          (res) => {
            this.isShowSuccessDialog = true;
            emit("on-close-check-dialog");
          },
          (err) => {
            this.isShowFailDialog = true;
            emit("on-close-check-dialog");
          })
      },
      closeFail(){
        this.isShowFailDialog = false ;
      },
      closeSuc(){
        this.isShowSuccessDialog = false ;
      }
//      toOrderList () {
//        this.$router.push({path: '/orderList'})
//      }
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>

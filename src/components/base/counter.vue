<template>
  <div class="counter-component">
    <div class="counter-show">
      <input type="number" v-model="number" @change="fixNumber">
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      max: {
        type: Number,
        default: 5
      },
      min: {
        type: Number,
        default: 1
      }
    },
    data () {
      return {
        number: this.min
      }
    },
    watch: {
      number () {
        this.$emit('on-change', this.number)
      }
    },
    methods: {
      fixNumber () {
        let fix
        if (typeof this.number === 'string') {
          fix = Number(this.number.replace(/\D/g, ''))
        }
        else {
          fix = this.number
        }
        if (fix > this.max || fix < this.min) {
          fix = this.min
        }
        this.number = fix
      },
    }
  }
</script>


<style scoped>
  .counter-component {
    position: relative;
    display: inline-block;
    overflow: hidden;
    vertical-align: middle;
  }
  .counter-show {
    float: left;
  }
  .counter-show input {
    border: none;
    border-top: 1px solid #e3e3e3;
    border-bottom: 1px solid #e3e3e3;
    height: 23px;
    line-height: 23px;
    width: 30px;
    outline: none;
    text-indent: 4px;
  }
  .counter-btn {
    border: 1px solid #e3e3e3;
    float: left;
    height: 25px;
    line-height: 25px;
    width: 25px;
    text-align: center;
    cursor: pointer;
  }
  .counter-btn:hover {
    border-color: #4fc08d;
    background: #4fc08d;
    color: #fff;
  }
  input{
    width: 50px!important;
  }

</style>

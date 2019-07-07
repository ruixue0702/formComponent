<template>
    <div class="x_formItem">
      <label v-if="label" class="x_label" :style="{width: labelWidth ? labelWidth: form.labelWidth ? form.labelWidth : 'auto'}">{{label}}</label>
      <div class="x_errorBox">
        <slot></slot>
        <div class="x_errorMessage" :class="errorMessage ? 'x_emShow' : ''">{{errorMessage}}</div>
      </div>
    </div>
</template>

<script>
  import Schema from 'async-validator'
  export default {
    provide() {
        return {
            formItem: this
        }
    },
    inject: ["form"],
    props: {
      label: {
        type: String,
        default: ""
      },
      labelWidth: {
        type: String,
        default: ""
      },
      prop: {
        type: String
      }
    },
    data() {
      return {
        errorMessage: "",
        isError: false
      };
    },
    mounted() {
      this.$on("validate", () => {
          this.validate();
      });
      this.$on('focus',()=>{
        this.errorMessage = ""
        this.isError = false
      })
    },
    methods: {
        validate() {
            // 做校验
            const value = this.form.model[this.prop];
            const rules = this.form.rules[this.prop];
            // npm i async-validator -S
            const desc = { [this.prop]: rules };
            const schema = new Schema(desc);
            // return的是校验结果的Promise
            return schema.validate({ [this.prop]: value }, errors => {
                if (errors) {
                    this.errorMessage = errors[0].message;
                    this.isError = true
                } else {
                    this.errorMessage = "";
                    this.isError = false
                }
            });
        }
    },
  };
</script>
<style>
  .x_errorMessage { 
    color: rgba(245,100,100,1);
    position: absolute;
    bottom: 0;
    padding-left: 12px;
    opacity: 0;
    transition: opacity 0.3s ease-in-out , transform 0.3s ease-in-out;
    -webkit-transition: opacity 0.3s ease-in-out ,  -webkit-transform 0.3s ease-in-out;
    transform: translateY(10px);
    -ms-transform: translateY(10px); /* IE 9 */
    -webkit-transform: translateY(10px); /* Safari and Chrome */
    height: 32px;
    line-height: 32px;
    font-size: 12px;
    box-sizing: border-box;
  }
  .x_errorMessage.x_emShow {
    opacity: 1;
    transform: translateY(32px);
    -ms-transform: translateY(32px); /* IE 9 */
    -webkit-transform: translateY(32px); /* Safari and Chrome */
  }
  .x_formItem {
    width: 100%;
    height: auto;
    box-sizing: border-box;
  }
  .x_errorBox {
    position: relative;
    width: auto;
    height: auto;
    display: inline-block;
    vertical-align: top;
    box-sizing: border-box;
  }
  .x_label {
    display: inline-block;
    vertical-align: top;
    width: auto;
    height: 32px;
    line-height: 32px;
    padding: 0 12px;
    box-sizing: border-box;
  }
</style>

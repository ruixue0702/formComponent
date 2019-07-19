<template>
  <div class="box" v-if="isShow">
    <p class="box-content">{{message}}</p>
  </div>
</template>

<script>
export default {
  props: {
    message: {
      type: String,
      default: ""
    },
    duration: {
      type: Number,
      default: 1000
    }
  },
  data() {
    return {
      isShow: false
    };
  },
  mounted(){
    console.log(this.title,this.message,this.duration)
  },
  methods: {
    show() {
      this.isShow = true;
      setTimeout(this.hide, this.duration);
    },
    hide() {
      this.isShow = false;
      this.remove();
    }
  }
};
</script>

<style scoped>
.box {
  position: fixed;
  width: 100%;
  top: 16px;
  left: 0;
  text-align: center;
  pointer-events: none;
  box-sizing: border-box;
}
.box-content {
  width: 200px;
  margin: 10px auto;
  font-size: 14px;
  border: blue 1px solid;
  padding: 8px 16px;
  background: #fff;
  border-radius: 4px;
  margin-bottom: 8px;
}
</style>
<template>
  <div class="child">
    <button @click="changeInfo">改变info的值</button>
    <button @click="changeMsg">改变msg的值</button>
  </div>
</template>

<script>
export default {
  name: "child",
  props: {
    info: {
      type: Object,
      default: function() {
        return {};
      },
    },
    msg: {
      type: String,
      default: "",
    },
  },
  data: function() {
    return {
      childInfo: this.info,
      childMsg: this.msg,
    };
  },
  methods: {
    changeInfo() {
      this.childInfo.name = "libai";
      console.log("childInfo", this.childInfo, this.info);
    },
    changeMsg() {
      this.childMsg = "我是子组件改变的值";
      console.log("childInfo", this.childMsg, this.msg);
    },
  },
};
</script>
<style scoped></style>

<template>
  <div class="wrapper">
    123
    {{ name }}
    {{ age }}
    {{info.name}}
    {{msg}}
    {{cy}}
    <child :info="info" :msg="msg"></child>
  </div>
</template>

<script>
import axios from "axios";
import child from "./components/child.vue";
export default {
  name: "App",
  data: function() {
    return {
      age1: 10,
      age2: 20,
      name: "xubu",
      chengyu: [],
      info: {
        name: "xubu",
        age: 28,
      },
      abc:'',
      msg:'我的父组件的值',
    };
  },
  watch: {
    info: function(oldValue, newValue) {
      console.log("oldValue", oldValue);
      console.log("newValue", newValue);
    },
  },
  computed: {
    cy(){
      console.log('---------',this.chengyu)
      return this.chengyu.join(',')
    }
  },
  components: {
    child,
  },
  created() {
    let that = this
    that.getCy().then((res) => {
      console.log("xubu", res,Object.prototype.toString.call(res));
      that.chengyu = res
      console.log('-----chengyu----',that.chengyu,res,that.chengyu.join(','))
    });
    console.log('aaaaa',this.info);
  },
  methods: {
    getCy() {
      return new Promise((resolve) => {
        axios
          .get("/api/idiomJie/query", {
            params: {
              wd: "天天向上",
              size: 5,
              key: "056a735c7ddb375dd615ccfc3584144e",
            },
          })
          .then(function(response) {
            console.log("response", response, response.data.result.data[0]);
            resolve(response.data.result.data);
          });
      });
    },
  },
};
</script>

<style></style>

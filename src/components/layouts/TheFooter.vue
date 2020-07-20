<template>
  <div class="footer">
    <div class="container">
      <button
        type="button"
        v-clipboard:copy="message"
        v-clipboard:success="onCopy"
        v-clipboard:error="onError"
      >微信</button>
      <button @click="qqopen">QQ</button>
      <button @click="githubopen">github</button>
    </div>
  </div>
</template>

<script>
import Clipboard from "clipboard";
export default {
  name: "TheFooter",
  data() {
    return {
      message: "L_Nut547"
    };
  },
  methods: {
    // weixinopen() {
    //   console.log(1);
    //   let clipboard = new Clipboard(".copy_btn", {
    //     text: function() {
    //       return data.url;
    //     }
    //   });
    //   clipboard.on("success", e => {
    //     this.$message({
    //       message: "复制成功",
    //       showClose: true,
    //       type: "success"
    //     });
    //     // 释放内存
    //     clipboard.destroy();
    //   });
    //   clipboard.on("error", e => {
    //     this.$message({ message: "复制失败,", showClose: true, type: "error" });
    //     clipboard.destroy();
    //   });
    // },
    onCopy: function(e) {
      alert("You just copied: " + e.text);
    },
    onError: function(e) {
      alert("Failed to copy texts");
    },
    qqopen() {
      window.location.href =
        "http://wpa.qq.com/msgrd?v=3&uin=1226222530&site=qq&menu=yes";
    },
    githubopen() {
      window.location.href = "https://github.com/lgs1226222530";
    }
  }
};
</script>

<style>
</style>
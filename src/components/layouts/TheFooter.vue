<template>
  <div class="footer">
    <div class="container">
      <p>
        <button
          type="button"
          class="btn btn-success btn-circle"
          v-clipboard:copy="message"
          v-clipboard:success="onCopy"
          v-clipboard:error="onError"
        >
          <i class="fa fa-wechat"></i>
        </button>&nbsp;
        <button type="button" class="btn btn-info btn-circle" @click="qqopen">
          <i class="fa fa-qq"></i>
        </button>&nbsp;
        <button type="button" class="btn btn-default btn-circle" @click="githubopen">
          <i class="fa fa-github-alt"></i>
        </button>
      </p>
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
    onCopy: function(e) {
      alert("已经帮您复制微信 " + e.text);
    },
    onError: function(e) {
      alert("复制失败");
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
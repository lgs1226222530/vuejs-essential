<template>
  <div class="col-md-9 left-col">
    <div class="panel panel-default padding-md">
      <div class="panel-body">
        <h2>
          <i class="fa fa-cog"></i> 编辑个人资料
        </h2>
        <hr />
        <div class="form-horizontal" data-validator-form>
          <div class="form-group">
            <label class="col-sm-2 control-label">用户名</label>
            <div class="col-sm-6">
              <input
                v-model.trim="username"
                v-validator:input.required="{ title: '用户名', regex: /^[a-zA-Z]+\w*\s?\w*$/, error: '用户名要求以字母开头的单词字符' }"
                type="text"
                class="form-control"
              />
            </div>
          </div>
          <div class="form-group">
            <label class="col-sm-2 control-label">性别</label>
            <div class="col-sm-6">
              <select v-model="sex" class="form-control">
                <option value>未选择</option>
                <option value="male">男</option>
                <option value="female">女</option>
              </select>
            </div>
          </div>
          <div class="form-group">
            <label class="col-sm-2 control-label">填写兴趣</label>
            <div class="col-sm-6">
              <input
                placeholder="点击回车增加兴趣"
                @keyup.enter="addInterest(hobby)"
                type="text"
                class="form-control"
                v-model="hobby"
              />
            </div>
          </div>
          <div class="form-group">
            <label class="col-sm-2 control-label">兴趣</label>
            <div class="col-sm-6">
              <ul>
                <li
                  v-for="hobby in hobbies"
                  :key="hobby"
                  class="tag-style"
                  :title="'点击移除兴趣：'+hobby"
                  @click="removeInterest(hobby)"
                >
                  <button type="button" class="btn btn-default">{{ hobby }}</button>
                </li>
              </ul>
            </div>
          </div>
          <div class="form-group">
            <label class="col-sm-2 control-label">个人简介</label>
            <div class="col-sm-6">
              <textarea v-model.trim="introduction" type="text" class="form-control"></textarea>
            </div>
          </div>

          <div class="form-group">
            <div class="col-sm-offset-2 col-sm-6">
              <button type="submit" class="btn btn-primary" @click="updateProfile">应用修改</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "EditProfile",
  data() {
    return {
      username: "", // 用户名
      sex: "", // 性别
      hobby: "",
      hobbies: [], // 兴趣
      introduction: "" // 个人简介
    };
  },
  created() {
    const user = this.$store.state.user;
    if (user && typeof user === "object") {
      const { name, sex, hobbies, introduction } = user;
      this.username = name;
      this.sex = sex || this.sex;
      this.hobbies = hobbies || this.hobbies;
      this.introduction = introduction;
    }
  },
  methods: {
    updateProfile(e) {
      setTimeout(() => {
        if (e.target.canSubmit) {
          this.$store.dispatch("updateUser", {
            name: this.username,
            sex: this.sex,
            hobbies: this.hobbies,
            introduction: this.introduction
          });
          // 删除 alert，使用实例的 $message 的 show 方法
          this.$message.show("修改成功");
        }
      });
    },
    addInterest(hobby) {
      this.hobby = "";
      hobby = hobby.replace(/[\s#]+/g, "");
      if (this.hobbies.includes(hobby)) {
        alert("已有该兴趣");
      } else if (hobby) {
        this.hobbies.push(hobby);
      }
    },
    removeInterest(hobby) {
      for (let i of this.hobbies.keys()) {
        if (this.hobbies[i] === hobby) {
          this.hobbies.splice(i, 1);
          break;
        }
      }
    }
  }
};
</script>

<style scoped>
.form-group ul,
.form-group ul li {
  padding-inline-start: 0;
  list-style: none;
  display: inline;
}
.form-group ul li button {
  margin: 0px 2px 2px 0px;
}
</style>
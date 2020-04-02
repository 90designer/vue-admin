<template>
  <div id="login">
    <div class="login-wrap">
      <ul class="menu-tab">
        <li
          :class="{ current: item.isActive }"
          v-for="item in menutab"
          :key="item.id"
          @click="toggleMenu(item)"
        >
          {{ item.txt }}
        </li>
      </ul>
      <!-- 表单start -->
      <el-form
        :model="ruleForm"
        status-icon
        :rules="rules"
        ref="ruleForm"
        class="login-form"
      >
        <el-form-item prop="pass" class="form-item-list">
          <label>邮箱</label>
          <el-input
            type="password"
            v-model="ruleForm.pass"
            autocomplete="off"
          ></el-input>
        </el-form-item>
        <el-form-item prop="checkPass" class="form-item-list">
          <label>密码</label>
          <el-input
            type="password"
            v-model="ruleForm.checkPass"
            autocomplete="off"
          ></el-input>
        </el-form-item>
        <el-form-item prop="age" class="form-item-list">
          <label>验证码</label>
          <el-row :gutter="8">
            <el-col :span="14"
              ><div class="grid-content bg-purple">
                <el-input v-model.number="ruleForm.age"></el-input></div
            ></el-col>
            <el-col :span="10"
              ><div class="grid-content bg-purple">
                <el-button type="success" class="block">获取验证码</el-button>
              </div></el-col
            >
          </el-row>
        </el-form-item>
        <el-form-item>
          <el-button
            type="primary"
            @click="submitForm('ruleForm')"
            class="login-submit block"
            >登陆</el-button
          >
        </el-form-item>
      </el-form>
      <!-- 表单end -->
    </div>
  </div>
</template>
<script>
export default {
  name: "login",
  data() {
    var checkAge = (rule, value, callback) => {
      if (!value) {
        return callback(new Error("年龄不能为空"));
      }
      setTimeout(() => {
        if (!Number.isInteger(value)) {
          callback(new Error("请输入数字值"));
        } else {
          if (value < 18) {
            callback(new Error("必须年满18岁"));
          } else {
            callback();
          }
        }
      }, 1000);
    };
    var validatePass = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请输入密码"));
      } else {
        if (this.ruleForm.checkPass !== "") {
          this.$refs.ruleForm.validateField("checkPass");
        }
        callback();
      }
    };
    var validatePass2 = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请再次输入密码"));
      } else if (value !== this.ruleForm.pass) {
        callback(new Error("两次输入密码不一致!"));
      } else {
        callback();
      }
    };
    return {
      menutab: [
        { txt: "登陆", isActive: true },
        { txt: "注册", isActive: false }
      ],
      ruleForm: {
        pass: "",
        checkPass: "",
        age: ""
      },
      rules: {
        pass: [{ validator: validatePass, trigger: "blur" }],
        checkPass: [{ validator: validatePass2, trigger: "blur" }],
        age: [{ validator: checkAge, trigger: "blur" }]
      }
    };
  },
  created() {},
  mounted() {},
  methods: {
    toggleMenu: function(data) {
      this.menutab.forEach(ele => {
        ele.isActive = data.isActive;
      });

      data.isActive = !data.isActive;
    },
    submitForm(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    }
  }
};
</script>
<!--scoped 当前文件有效-->
<style lang="scss" scoped>
#login {
  // vh 可是区域的百分比
  height: 100vh;
  background-color: #344a5f;
}
.login-wrap {
  width: 330px;
  margin: auto;
}
.menu-tab {
  text-align: center;
  li {
    display: inline-block;
    width: 88px;
    line-height: 36px;
    font-size: 14px;
    color: #fff;
    border-radius: 2px;
    cursor: pointer;
  }
  .current {
    background-color: rgba(0, 0, 0, 0.1);
  }
}
.login-form {
  label {
    display: block;
    font-size: 14px;
    color: #fff;
  }
  margin-top: 30px;
  .form-item-list {
    margin-bottom: 13px;
    input {
      height: 40px;
      line-height: 40px;
    }
  }
  .block {
    display: block;
    width: 100%;
  }
  .login-submit {
    margin-top: 10px;
  }
}
</style>

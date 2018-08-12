<template>
  <div class="login">
    <div class="logo margin">
      <img src="https://s10.mogucdn.com/p1/160408/upload_ie4gkmjvgvqtiytdg4zdambqgiyde_220x52.png" alt="">
      <span>{{$t("login.logo.span")}}</span>
    </div>
    <div class="content margin">
      <div class="bg">
        <el-select v-model="langValue" class="language_selection" @change="onChangeLang">
          <el-option
            v-for="item in langOptions"
            :key="item.value"
            :label="item.label"
            :value="item.value">
          </el-option>
        </el-select>
      </div>
      <el-tabs v-model="activeName" @tab-click="handleClick" class="login-box-warp" style="width: 320px;height: 350px;text-align: center">
        <el-tab-pane :label="$t('login.content.commonlogin')" name="first">
          <el-form :model="ruleForm" :rules="rules" ref="ruleForm">
            <el-form-item label="" prop="username">
              <el-input :placeholder="$t('login.username.placeholder')" type="text" v-model="ruleForm.username"></el-input>
            </el-form-item>
            <el-form-item label="" prop="password">
              <el-input :placeholder="$t('login.password.placeholder')" type="password" v-model="ruleForm.password"></el-input>
            </el-form-item>
            <el-form-item>
              <el-button type="primary" style="width: 320px" @click="submitForm('ruleForm')">{{$t('login')}}</el-button>
            </el-form-item>
          </el-form>
        </el-tab-pane>
        <el-tab-pane :label="$t('login.content.mobilelogin')" name="second">
          <el-form :model="ruleForm" :rules="rules" ref="ruleForm">
            <el-form-item label="" prop="username">
              <el-input :placeholder="$t('login.username.placeholder')" type="text" v-model="ruleForm.username"></el-input>
            </el-form-item>
            <el-form-item label="" prop="password">
              <el-input :placeholder="$t('login.password.placeholder')" type="password" v-model="ruleForm.password"></el-input>
            </el-form-item>
            <el-form-item>
              <el-button type="primary" style="width: 320px" @click="submitForm('ruleForm')">{{$t('login')}}</el-button>
            </el-form-item>
          </el-form>
        </el-tab-pane>
      </el-tabs>
    </div>
  </div>
</template>
<style>
  .login>.logo{padding: 20px 0}
  .login>.logo>span {
    display: inline-block;
    width: 861px;
    background-color: #ffefef;
    border: 1px solid #ffc0cc;
    text-align: center;
    line-height: 28px;
    font-size: 11px;
    color: #666;
    transform: translateY(-20px);
  }
  .login>.content{
    height: 600px;
    position: relative;
  }
  .login>.content>.bg{
    position: absolute;
    width: 1920px;height:600px;
    background-image: url("https://s17.mogucdn.com/p2/170105/upload_541i9di2b3icf9j13f24e0bg7b1i6_1920x600.png");
    margin-left: 50%;
    transform: translateX(-50%);
  }
  .login>.content>.bg>.language_selection{
    left: 1250px;
    top: 20px;
  }

  .login>.content>.login-box-warp{
    position: absolute;
    top: 80px;
    left: 760px;
    background-color: #ffeceb;
    opacity: .9;
    padding: 0 45px;
  }
  .login>.content>.login-box-warp .el-tabs__nav{height: 55px}
  .login>.content>.login-box-warp .el-tabs__nav>#tab-first{line-height: 55px;font-weight: 700}
  .login>.content>.login-box-warp .el-tabs__nav>#tab-second{line-height: 55px;font-weight: 700}
</style>
<script>
  import {mapActions,mapGetters} from 'vuex'
  export default {
    created(){
      this.langValue = this.langCode
    },
    mounted(){
      document.getElementsByClassName("el-tabs__nav")[0].style.transform = "translateX(50px)";
    },
    data() {
      return {
        activeName: 'second',
        ruleForm: {
          username: '',
          password: ''
        },
        rules: {
          username: [
            // { validator: validatePass, trigger: 'blur' }
          ],
          password: [
            // { validator: validatePass, trigger: 'blur' }
          ],
        },
        langOptions: [{
          value: 'zh',
          label: '中文'
        }, {
          value: 'en',
          label: 'English'
        }],
        langValue: ""
      };
    },
    methods: {
      submitForm(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
            alert('submit!');
            this.$router.push({path:"/home"})
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
      resetForm(formName) {
        this.$refs[formName].resetFields();
      },
      handleClick(tab, event) {
        console.log(tab, event);
      },
      onChangeLang(){
        this.changeLang(this.langValue)
        window.location.reload()
      },
      ...mapActions(["changeLang"])
    },
    computed:{
      ...mapGetters(["langCode"])
    }
  }
</script>

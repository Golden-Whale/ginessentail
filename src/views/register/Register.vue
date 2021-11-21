<template>
  <div class="register">
    <b-row class="mt-5">
      <b-col
        md="8"
        offset-md="2"
        lg="6"
        offset-lg="3"
      >
        <b-card title="注册">
          <b-form>
            <b-form-group label="姓名:">
              <b-form-input
                v-model="$v.user.userName.$model"
                type="text"
                placeholder="输入您的名称(选填)"
              ></b-form-input>
            </b-form-group>
            <b-form-group label="手机号:">
              <b-form-input
                v-model="$v.user.telephone.$model"
                type="number"
                placeholder="输入手机号"
              ></b-form-input>
              <b-form-invalid-feedback :state="validateState('telephone')">
                手机号格式有误
              </b-form-invalid-feedback>
              <b-form-valid-feedback :state="validateState('telephone')">
                手机号符合 11 位
              </b-form-valid-feedback>
            </b-form-group>
            <b-form-group label="密码:">
              <b-form-input
                v-model="$v.user.password.$model"
                type="password"
                placeholder="输入密码"
              ></b-form-input>
              <b-form-invalid-feedback :state="validateState('password')">
                密码不能小于6位
              </b-form-invalid-feedback>
            </b-form-group>
            <b-form-group>
              <b-button
                variant="outline-primary"
                block
                @click="register"
              >注册</b-button>
            </b-form-group>
          </b-form>
        </b-card>
      </b-col>
    </b-row>
  </div>
</template>

<script>
import { required, numeric, minLength } from 'vuelidate/lib/validators';
import customValidator from '@/helper/validator';

export default {
  data() {
    return {
      user: {
        userName: '',
        telephone: '',
        password: '',
      },
      validation: null,
    };
  },
  validations: {
    user: {
      userName: {},
      telephone: {
        required,
        numeric,
        telethone: customValidator.telephoneValidator,
      },
      password: {
        required,
        minLength: minLength(6),
      },
    },
  },
  methods: {
    validateState(name) {
      // es6的结构赋值
      const { $dirty, $error } = this.$v.user[name];
      return $dirty ? !$error : null;
    },
    register() {
      console.log('register');
      console.log(this.user.telephone.search(/1[2-9]\d{9}/));
      if (this.user.telephone.search(/1[3-9]\d{9}/)) {
        this.validation = false;
      } else {
        this.validation = true;
      }
    },
  },
};
</script>

<style></style>

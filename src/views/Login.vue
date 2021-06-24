<template>
  <div>
    <form @submit.prevent="loginAction">
      <div>
        <input type="email" v-model="form.email" @keyup="updateEmail" />
      </div>
      <div>
        <input type="password" v-model="form.password" @keyup="updatePw" />
      </div>
      <div>
        <button class="login_btn" :disabled="!isValid" @click="loginAction">
          Login
        </button>
      </div>
    </form>
  </div>
  <!-- 회원가입 이름 / 암호 / 이메일 / 성별 -->
</template>

<script>
export default {
  data() {
    return {
      form: {
        email: null,
        password: null,
      },
      isValid: false,
      isValidEmail: false,
      isValidPw: false,
    };
  },
  methods: {
    updateEmail() {
      this.isValidEmail = this.validateEmail(this.form.email);
      this.isValid = this.isValidEmail && this.isValidPw;
    },
    updatePw() {
      this.isValidPw = this.form.password.length > 5;
      this.isValid = this.isValidEmail && this.isValidPw;
    },
    validateEmail(email) {
      const re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return re.test(String(email).toLowerCase());
    },
    loginAction() {
      //1.서버랑 통신
      //2.서버에서 성공이라고 하면 홈으로 이동
      //3. 아니면 에러메세지 보여줌!
      this.$router.push("/");
    },
  },
};
</script>

<style scoped>
.login_btn {
  background: orange;
  padding: 10px;
}
.login_btn:disabled {
  background: #ddd;
}
</style>

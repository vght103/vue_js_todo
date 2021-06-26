<template>
  <div class="container">
    <h1>todos</h1>
    <form @submit.prevent="loginAction">
      <div class="row">
        <div class="col-xs-12 col-md-6 mb-2">
          <input
            type="email"
            class="form-control"
            v-model="form.email"
            @keyup="updateEmail"
            placeholder="email"
          />
        </div>
        <div class="col-xs-12 col-md-6 pr-2">
          <input
            type="password"
            class="form-control"
            v-model="form.password"
            @keyup="updatePw"
            placeholder="Passwordd"
          />
        </div>
      </div>
      <div>
        <button
          class="btn btn-primary"
          :disabled="!isValid"
          @click="loginAction"
        >
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
/* .login_btn {
  background: orange;
  padding: 12px 20px;
  border-radius: 5px;
}
.login_btn:disabled {
  background: #ddd;
}

h1 {
  width: 100%;
  font-size: 100px;
  font-weight: 100;
  text-align: center;
  color: rgba(175, 47, 47, 0.15);
  -webkit-text-rendering: optimizeLegibility;
  -moz-text-rendering: optimizeLegibility;
  text-rendering: optimizeLegibility;
}

input {
  width: 180px;
  height: 20px;
}

form {
  text-align: center;
}

div {
  margin: 20px 0; */
/* } */
</style>

<template>
  <div>
    <form @submit.prevent="registerAction">
      <div class="u_info">
        <span>이름</span>
        <input type="text" v-model="form.name" @keyup="updateName" />
      </div>

      <div class="u_info">
        <span>아이디</span>
        <input type="text" v-model="form.id" @keyup="updateId" />
      </div>

      <div class="u_info">
        <span>패스워드</span>
        <input type="password" v-model="form.password" @keyup="updatePw" />
      </div>

      <div class="u_info">
        <span>이메일</span>
        <input type="email" v-model="form.email" @keyup="updateEmail" />
      </div>

      <div class="u_info">
        <span class="gender">성별</span>
        <div class="gender">
          <input type="radio" id="male" name="gender" />
          <label for="male">남자</label>
        </div>
        <div class="gender">
          <input type="radio" id="female" name="gender" />
          <label for="female">여자</label>
        </div>
      </div>

      <div>
        <button
          class="register_btn"
          :disabled="!isValid"
          @click="registerAction"
        >
          회원가입
        </button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: null,
        id: null,
        password: null,
        email: null,
      },

      isValid: false,
      isValidName: false,
      isValidId: false,
      isValidPw: false,
      isValidEmail: false,
    };
  },

  methods: {
    updateName() {
      this.isValidName = this.form.name.length > 3;
      this.isValid =
        this.isValidName &&
        this.isValidId &&
        this.isValidPw &&
        this.isValidEmail;

      console.log(this.isValidName);
    },
    updateId() {
      this.isValidId = this.form.id.length > 6;
      this.isValid =
        this.isValidName &&
        this.isValidId &&
        this.isValidPw &&
        this.isValidEmail;
      console.log(this.isValidId);
    },
    updatePw() {
      this.isValidPw = this.form.password.length > 5;
      this.isValid =
        this.isValidName &&
        this.isValidId &&
        this.isValidPw &&
        this.isValidEmail;
      console.log(this.isValidPw);
    },
    updateEmail() {
      this.isValidEmail = this.validateEmail(this.form.email);
      this.isValid =
        this.isValidName &&
        this.isValidId &&
        this.isValidPw &&
        this.isValidEmail;
      console.log(this.isValidEmail);
    },

    validateEmail(email) {
      const re = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return re.test(String(email).toLowerCase());
    },

    registerAction() {
      this.$router.push("/");
    },
  },
};
</script>

<style scoped>
span {
  display: inline-block;
  width: 100px;
}

.u_info {
  margin-bottom: 20px;
}

.gender {
  display: inline-block;
}

.register_btn {
  border: 1px solid gray;
  padding: 8px;
  background-color: pink;
}

.register_btn:disabled {
  background-color: #ddd;
}
</style>

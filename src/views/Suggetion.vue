<template>
  <h1>USER 의견</h1>
  <div>
    <form @submit.prevent="submitAction">
      <div>
        <h3>
          이름
        </h3>
        <input
          v-model="form.name"
          @keyup="updateName"
          placeholder="이름을 입력해주세요"
        />
      </div>

      <div>
        <h3>
          패스워드
        </h3>
        <input
          v-model="form.password"
          @keyup="updatePassword"
          type="password"
          placeholder="비밀번호를 입력해주세요"
        />
      </div>

      <div>
        <h3>
          건의사항
        </h3>
        <textarea
          v-model="form.suggestions"
          @keyup="updateSuggetions"
          cols="30"
          rows="10"
          placeholder="내용을 입력해주세요"
        ></textarea>
      </div>

      <div>
        <button :disabled="!isValid" @click="submitAction">전송하기</button>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: "",
        password: "",
        suggestions: "",
      },

      isValid: "",
      isValidName: "",
      isValidPw: "",
      isValidSuggetions: "",
    };
  },

  methods: {
    updateName() {
      this.isValidName = this.form.name.length > 2;
      this.isValid =
        this.isValidName && this.isValidPw && this.isValidSuggetions;
      console.log(this.isValidName);
    },

    updatePassword() {
      this.isValidPw = this.form.password.length > 5;
      this.isValid =
        this.isValidName && this.isValidPw && this.isValidSuggetions;
      console.log(this.isValidPw);
    },

    updateSuggetions() {
      this.isValidSuggetions = this.form.suggestions.length > 20;
      this.isValid =
        this.isValidName && this.isValidPw && this.isValidSuggetions;
      console.log(this.isValidSuggetions);
    },

    submitAction() {
      this.$router.push("/");
    },
  },
};
</script>

<style scoped>
* {
  margin: 0;
  padding: 0;
  list-style: none;
}

h1 {
  text-align: center;
  margin-bottom: 40px;
}

h3 {
  margin-bottom: 10px;
}

div {
  text-align: center;
  margin: 20px 0;
}

input {
  width: 200px;
  padding: 5px;
}

button {
  background-color: plum;
  padding: 12px 20px;
}

button:disabled {
  background-color: #ddd;
}
</style>

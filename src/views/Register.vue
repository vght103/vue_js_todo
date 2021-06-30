<template>
  <h1>todos</h1>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Navbar</a>
        <button
          class="navbar-toggler"
          type="button"
          data-bs-toggle="collapse"
          data-bs-target="#navbarSupportedContent"
          aria-controls="navbarSupportedContent"
          aria-expanded="false"
          aria-label="Toggle navigation"
        >
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav me-auto mb-2 mb-lg-0">
            <li class="nav-item">
              <a class="nav-link active" aria-current="page" href="#">Home</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#">Link</a>
            </li>
            <li class="nav-item dropdown">
              <a
                class="nav-link dropdown-toggle"
                href="#"
                id="navbarDropdown"
                role="button"
                data-bs-toggle="dropdown"
                aria-expanded="false"
              >
                Dropdown
              </a>
              <ul class="dropdown-menu" aria-labelledby="navbarDropdown">
                <li><a class="dropdown-item" href="#">Action</a></li>
                <li><a class="dropdown-item" href="#">Another action</a></li>
                <li><hr class="dropdown-divider" /></li>
                <li>
                  <a class="dropdown-item" href="#">Something else here</a>
                </li>
              </ul>
            </li>
            <li class="nav-item">
              <a
                class="nav-link disabled"
                href="#"
                tabindex="-1"
                aria-disabled="true"
                >Disabled</a
              >
            </li>
          </ul>
          <form class="d-flex">
            <input
              class="form-control me-2"
              type="search"
              placeholder="Search"
              aria-label="Search"
            />
            <button class="btn btn-outline-success" type="submit">
              Search
            </button>
          </form>
        </div>
      </div>
    </nav>
    <form @submit.prevent="registerAction" class="row justfy-content-center">
      <div class="u_info col-12 ">
        <span>이름</span>
        <input
          class="form-control"
          type="text"
          v-model="form.name"
          @keyup="updateName"
        />
      </div>

      <div class="u_info col-12 ">
        <span>아이디</span>
        <input
          class="form-control"
          type="text"
          v-model="form.id"
          @keyup="updateId"
        />
      </div>

      <div class="u_info col-12 ">
        <span>패스워드</span>
        <input
          class="form-control"
          type="password"
          v-model="form.password"
          @keyup="updatePw"
        />
      </div>

      <div class="u_info col-12 ">
        <span>이메일</span>
        <input
          class="form-control"
          type="email"
          v-model="form.email"
          @keyup="updateEmail"
        />
      </div>

      <div class="u_info col-12 ">
        <span class="gender">성별</span>
        <div class="gender">
          <input class="form-control" type="radio" id="male" name="gender" />
          <label for="male">남자</label>
        </div>
        <div class="gender">
          <input class="form-control" type="radio" id="female" name="gender" />
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
import axios from "axios";
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
      this.isValidName = this.form.name.length >= 2;
      this.isValid =
        this.isValidName &&
        this.isValidId &&
        this.isValidPw &&
        this.isValidEmail;

      console.log(this.isValidName);
    },
    updateId() {
      this.isValidId = this.form.id.length > 3;
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
      axios({
        url: "http://149.28.19.152:7500/user",
        method: "POST",
        data: {
          email: this.form.email,
          name: this.form.name,
          password: this.form.password,
        },
      })
        .then((res) => {
          if (res) {
            this.$router.push("/login");
          }
        })
        .catch((error) => {
          alert(error.message);
          console.error(error);
        });
    },
  },
};
</script>

<style scoped>
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

span {
  display: inline-block;
  width: 100px;
}

.u_info {
  margin-bottom: 20px;
}

.gender {
  display: inline-block;
  width: 80px;
}

.register_btn {
  border: 1px solid gray;
  padding: 12px 20px;
  background-color: pink;
  border: none;
  border-radius: 5px;
}

.register_btn:disabled {
  background-color: #ddd;
}

form {
  text-align: center;
}
</style>

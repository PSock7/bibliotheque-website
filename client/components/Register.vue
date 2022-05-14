<template>
  <div>
    <form @submit.prevent="createUser()">
      <div class="container">
        <form class="form">
          <div class="form__text">Register to Efrei Bibliotheque</div>

          <div class="form__group">
            <input
              type="text"
              class="form__input"
              placeholder="First name"
              id="first name"
              required
            />
            <label for="first name" class="form__label">First name</label>
          </div>

          <div class="form__group">
            <input
              type="text"
              class="form__input"
              placeholder="Last name"
              id="last name"
              required
            />
            <label for="last name" class="form__label">Last name</label>
          </div>

          <div class="form__group">
            <input
              type="email"
              class="form__input"
              placeholder="Email address"
              id="email"
              required
            />
            <label for="email" class="form__label">Email address</label>
          </div>

          <div class="form__group">
            <input
              type="password"
              class="form__input"
              placeholder="Password"
              id="password"
              required
            />
            <label for="password" class="form__label">Password</label>
          </div>
          <div class="form__button">
            <a href="#" class="btn">Submit</a>
          </div>
        </form>
      </div>
    </form>
  </div>
</template>

<script>
module.exports = {
  props: {
    articles: { type: Array, default: [] },
    panier: { type: Object },
  },
  data() {
    return {
      email: "",
      password: "",
    };
  },
  async mounted() {},
  methods: {
    async createUser() {
      await axios.post("/api/register", {
        email: this.email,
        password: this.password,
      });
      this.$router.push("/");
    },
  },
};
</script>

<style scoped>
.container {
  width: 400px;
  height: auto;
  border-radius: 2px;
  background: #09c2d7;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.3);

  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

.form {
  padding: 30px 35px;
  background: #fff;
  clip-path: polygon(0 0, 100% 0%, 100% 90%, 0% 100%);
}

.form__text {
  color: #000;
  font-size: 30px;
  text-align: center;
  margin-bottom: 20px;
  font-family: Cambria, Cochin, Georgia, Times, "Times New Roman", serif;
}

.form__input {
  cursor: pointer;
  display: block;
  font-size: 12px;
  width: 100%;
  background: #eeeeee;
  color: #000;
  /* margin-bottom: 10px; */
  padding: 15px;
  border-radius: 3px;

  border: none;
  border-bottom: 2px solid transparent;

  transition: all 0.3s;
}

.form__input:focus {
  outline: none;
  border-bottom: 2px solid #09c2d7;
}

.form__input::-webkit-input-placeholder {
  color: #777;
}

.form__label {
  display: block;
  height: 100%;
  width: 100%;
  color: #777;
  font-size: 12px;
  font-weight: bold;
  padding: 5px 15px;

  transition: all 0.2s;
}

.form__input:placeholder-shown + .form__label {
  transform: translateY(-37px);
  opacity: 0;
  visibility: hidden;
}

/* button style */
.form__button {
  text-align: center;
  margin-bottom: 10px;
}

.btn {
  display: inline-block;
  cursor: pointer;
  font-size: 15px;
  font-weight: bold;
  text-decoration: none;
  background-color: #eee;
  color: #2c2c2c;
  padding: 10px 30px;
  border-radius: 3px;

  transition: all 0.2s;
}

.btn:hover {
  background: #09c2d7;
  color: #fff;
  box-shadow: 0 20px 30px rgba(0, 0, 0, 0.25);
}
i:hover {
  box-shadow: 0 20px 30px rgba(0, 0, 0, 0.2);
  transform: translateY(-2px);
}

i:active {
  transform: translateY(0);
}
</style>

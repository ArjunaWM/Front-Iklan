<template>
  <div class="register-area ptb-100">
    <div class="container-fluid">
      <div class="row">
        <div class="col-md-12 col-12 col-lg-6 col-xl-6 ml-auto mr-auto">
          <div class="login">
            <div class="login-form-container">
              <div class="login-form">
                <form action="#" method="post" v-on:submit.prevent="Login">
                  <input type="text" name="user-email" placeholder="Email" v-model="email" />
                  <input
                    type="password"
                    name="user-password"
                    placeholder="Password"
                    v-model="password"
                  />
                  <div class="button-box">
                    <div class="login-toggle-btn">
                      <label>Belum terdaftar?</label>
                      <a href="/register">Sign up</a>
                    </div>
                    <!-- <button type="submit" class="default-btn floatright" value="login">Login</button> -->
                    <input type="submit" name="login" class="default-btn floatright" value="login" />
                  </div>
                </form>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        email: "",
        password: ""
      };
    },
    methods: {
      Login: function() {
        let email = this.email;
        let password = this.password;
        this.$store
          .dispatch("login", { email, password })
          .then(() => this.$router.push("/"))
          .catch(err => console.log(err));
      }
    }
  };
</script>
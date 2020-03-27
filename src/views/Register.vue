<template>
  <div class="register-area ptb-100">
    <div class="container-fluid">
      <div class="row">
        <div class="col-md-12 col-12 col-lg-12 col-xl-6 ml-auto mr-auto">
          <div class="login">
            <div class="login-form-container">
              <div class="login-form">
                <form action="#" method="post" v-on:submit.prevent="Register">
                  <input type="text" name="user-name" placeholder="Nama" v-model="nama" />
                  <input
                    type="password"
                    name="user-password"
                    placeholder="Password"
                    v-model="email"
                  />
                  <input name="user-email" placeholder="Email" type="email" v-model="password" />
                  <div class="button-box">
                    <input
                      type="submit"
                      name="register"
                      class="default-btn floatright"
                      value="register"
                    />
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
  module.exports = {
    data: function() {
      return {
        search: "",
        id: "",
        nama: "",
        email: "",
        password: "",
        action: "",
        message: "",
        currentPage: 1,
        rows: 0,
        perPage: 10,
        key: "",
        user: []
        //   fields: ["id", "nama", "email", , "Aksi"]
      };
    },
    methods: {
      Add: function() {
        this.action = "insert";
        this.nama = "";
        this.email = "";
        this.password = "";
      },
      Save: function() {
        let conf = { headers: { Authorization: "Bearer " + this.key } };
        this.$bvToast.show("loadingToast");
        if (this.action === "insert") {
          let form = new FormData();
          form.append("id", this.id);
          form.append("nama", this.nama);
          form.append("email", this.email);
          form.append("password", this.password);

          this.axios
            .post("/register", form, conf)
            .then(response => {
              this.$bvToast.hide("loadingToast");
              if (this.search == "") {
                this.getData();
              } else {
                this.searching();
              }
              this.message = response.data.message;
              this.$bvToast.show("message");
            })
            .catch(error => {
              console.log(error);
            });
        }
      }
    }
  };
</script>
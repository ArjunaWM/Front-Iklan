<template>
    <header>
        <div class="header-top-wrapper-2 border-bottom-2">
            <div class="header-info-wrapper pl-200 pr-200">
                <div class="electronics-login-register">
                    <ul>
                        <li><a href="#"><i class="pe-7s-users"></i>Admin</a></li>
                    </ul>
                </div>
                <div class="header-contact-info" @click="logout">
                    <ul>
                        <li><i class="pe-7s-shield"></i> <a href="/login">Logout</a></li>
                    </ul>
                </div>
            </div>
        </div>
        <div class="header-bottom pt-40 pb-30 clearfix">
            <div class="header-bottom-wrapper pr-200 pl-200">
                <div class="logo-3">
                    <a href="index.html">
                        <img src="assets/img/logo/logo-3.png" alt="">
                    </a>
                </div>
                <div class="product-tab-list3 text-center nav product-menu-mrg" role="tablist">
                    <a class="active" href="/" data-toggle="tab" role="tab">
                        <h4>Home</h4>
                    </a>
                    <a class="active" href="/iklan" data-toggle="tab" role="tab">
                        <h4>Tambah Iklan</h4>
                    </a>
                </div>
                <div class="categories-search-wrapper">
                    <div class="categories-wrapper">
                        <form action="#">
                            <input placeholder="Enter Your key word" type="text">
                            <button type="button"> Search </button>
                        </form>
                    </div>
                </div>
                <!-- <div class="trace-cart-wrapper">
                    <div class="categories-cart same-style">
                        <div class="same-style-icon">
                            <a href="#"><i class="pe-7s-cart"></i></a>
                        </div>
                        <div class="same-style-text">
                            <a href="cart.html">My Cart <br>0 Item</a>
                        </div>
                    </div>
                </div> -->
            </div>
        </div>
    </header>
</template>

<script>
export default {
    name: 'navbar',
    computed : {
        isLoggedIn : function(){ return this.$store.getters.isLoggedIn}
    },
    methods:{
      logout:function(){
          let conf = { headers : {"Authorization" : "Bearer " + localStorage.getItem("Authorization")} };
          let form = new FormData();
          this.axios.post('/logout', form, conf).then(response => {
            if (response.data.logged === false || response.data.status === 0) {
                this.$store.commit('logout')
                localStorage.removeItem("Authorization")
                this.$router.push({name: 'login'})
            }
          }).catch(error => {

        });
      },
  },
}
</script>
<template>
  <div class="authorization">
    <div class="blueAuth"></div>
    <div class="imgAuth">
      <img alt="Картинка для авторизации" src="../style/img/Auth.png">
    </div>
    <div class="authLogo">
      <img alt="Логотип OKR" src="../style/img/AuthLogo.png">
    </div>
    <div class="contAuth">
      <div class="authTitle">Вход</div>
      <form v-on:submit.prevent="onLog">
        <label for="signinEmail">E-mail</label>
        <input id="signinEmail" v-model="email" type="text" placeholder="E-mail" />
        <label for="signinPass">Пароль</label>
        <input id="signinPass" v-model="password" type="password" placeholder="Пароль" />
        <!-- <div class="errorMsg" v-if="this.$store.state.authHasError">Неверно введен email и/или пароль.</div> -->
        <div class="message">Еще не зарегистрированы?
          <router-link to="/signup">Создать аккаунт</router-link>
        </div>
        <button>Вход</button>
      </form>
    </div>
  </div>
</template>

<script>

export default {
  name: 'Signin',
  data: () => ({
    email: '',
    password: '',
  }),

  mounted: function () {
    this.$store.commit('resetErr');
  },

  methods: {
    async onLog()  {
      let user = {
        email: this.email,
        password: this.password
      }

      await this.$store.dispatch('login', user);
      if (!this.$store.state.authHasError) {
        this.$router.push('/');
      }
    },
  }
}
</script>
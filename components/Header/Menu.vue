<template>
  <div class="menu">
    <div class="menu__title" v-if="companyName || itn">
      {{ companyName }}
      <span>инн: {{itn}}</span>
    </div>
    <img src="@/assets/img/account.svg" class="menu-opener" alt="account" @click="openMenu=!openMenu"/>
    <transition name="bounce">
      <ul class="menu__items" v-if="openMenu == true">
          <li class="menu__list" v-if="$nuxt.$route.name == 'index'">
              <nuxt-link to="/user" class="menu__link" >Личные данные</nuxt-link>
          </li>
          <li class="menu__list">
              <a href="#" class="menu__link" @click.prevent="logout()">Выйти</a>
          </li>
      </ul>
    </transition>
    </div>
</template>

<script>
import resolveError from "../../helpers/resolveError";
export default {
  name: 'Menu',
  data(){
      return {
        openMenu: false,
      }
  },
  computed: {
    companyName() { return this.$store.state.user.user.company_name },
    itn() { return this.$store.state.user.user.itn }
  },
  methods: {
    logout() {
      this.$store.dispatch('logout')
      this.$router.push('/login')
    },
    closeMenuByClick(event){
      if (!event.target.classList.contains('menu') &&
        !event.target.closest('.menu')){
        this.openMenu = false
      }
    },
    closeMenuByEscape(event){
      if(event.key === "Escape") {
        this.openMenu = false
      }
    }
  },
  mounted(){
    this.$axios.get(process.env.baseUrl + '/lk/info')
        .then(response => {
            const responseData = response.data.data
            this.$store.dispatch('user/addUser', responseData)
        })
        .catch(function (e) {
            resolveError(e)
        })
    document.body.addEventListener('click', this.closeMenuByClick, false);
    document.addEventListener('keydown', this.closeMenuByEscape, false);
  },
  destroyed(){
    document.removeEventListener('keydown', this.closeMenuByEscape, false);
    document.body.removeEventListener('click', this.closeMenuByClick, false);
  }
};
</script>
<style lang="scss">
@import '@/styles/variables.scss';
.menu_ {
  display: flex;
  border-left: 1px solid #4a57d2;
  padding: 15px;
  color: $header-color;
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 265px;
  position: relative;
  box-sizing: border-box;
  @media(min-width: $tablet){
    border: 0;
    width: 320px;
    padding-right: 35px;
  }
  @media(min-width: $desktop){
    padding-right: 37px;
  }
  &__items{
    position: absolute;
    right: 15px;
    top: 16px;
    width: 280px;
    padding-left: 16px;
    background: #ffffff;
    box-shadow: 0px 5px 6px rgba(0, 0, 0, 0.2), 0px 3px 16px rgba(0, 0, 0, 0.12), 0px 9px 12px rgba(0, 0, 0, 0.14);
    border-radius: 4px;
    @media(min-width: $desktop){
      right: 37px;
    }
  }
  &__list{
      border-bottom: 1px solid #F2F2F2;
      padding: 14px 0;
    &:last-of-type{
        border-bottom: 0;
    }
  }
  &__link{
    font-size: 14px;
    display: block;
    padding: 10px 0;
    color: #1E1F23;
  }
  &__title {
    font-size: 12px;
    margin-left: 8px;
    letter-spacing: 0.004em;
    font-weight: normal;
    @media(min-width: $tablet){
      font-size: 14px;
      line-height: 20px;
      letter-spacing: normal;
    }
    span {
      font-size: 12px;
      line-height: 16px;
      letter-spacing: 0.7px;
      display: block;
    }
  }
  &-opener{
    cursor: pointer;
    position: absolute;
    right: 16px;
    @media(min-width: $tablet){
      right: 37px;
    }
  }
  .bounce-enter-active {
    animation: bounce-in .3s;
  }
    .bounce-leave-active {
      animation: bounce-in .3s reverse;
  }
  @keyframes bounce-in {
      0% {
        transform: scale(0);
      }
      50% {
        transform: scale(1.1);
      }
      100% {
        transform: scale(1);
      }
    }
}
</style>

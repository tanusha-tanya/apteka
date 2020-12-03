<template>
  <div id="header">
    <header class="header">
      <div class="header-menu">
        <a class="hamburger" href="#" @click.prevent="openMenu = !openMenu">
          <svg-icon name="burger" width="24" height="17" />
        </a>
      </div>
        <nuxt-link class="logo" to="/">
          <img
          src="@/assets/img/logo.svg"
          alt="Логотип"
          class="logo__img logo__img--big"
          />
        </nuxt-link>
      <div class="header-notice">  
        <a class="notice-link" href="#" @click.prevent="openNotice = true">
          <svg-icon name="notification" width="24" height="24" />
        </a> 
        <transition name="slide-fade"> 
          <Mynotice v-if="openNotice"/>
        </transition>
      </div>  
      <nuxt-link class="header-account" to="user">
        <svg-icon name="account_black" width="24" height="24" />
        <div class="header-title" v-if="companyName || itn">
          {{ companyName }}
          <span>инн: {{itn}}</span>
        </div>
      </nuxt-link>   
    </header>    
    <transition name="slide-fade">
      <div class="menu" v-if="openMenu">
        <nuxt-link to="/" class="menu-link" exact>
          <svg-icon name="home" width="24" height="24" />
        </nuxt-link>
        <nuxt-link to="/appeals" class="menu-link" exact>
          <svg-icon name="message" width="24" height="24" />
        </nuxt-link>
      </div>
    </transition> 
  </div>
</template>

<script>
import Logo from '@/components/Header/Logo';
import Menu from '@/components/Header/Menu';
import Mynotice from '@/components/Mynotice';
export default {
  name: 'Header',
  components: {
    Logo,
    Menu,
    Mynotice
  },
  data(){
    return{
      openMenu: false,
      openNotice: false
    }
  },
  computed: {
    isAuthorized(){
      return this.$route.name === 'index' || this.$route.name === 'User'
    },
    companyName() { return /*this.$store.state.user.user.company_name*/ 'ООО «Современная Фармацевтика»'},
    itn() { return /*this.$store.state.user.user.itn*/ '781 018 0435'}
  },
  methods:{
    closeMenuByClick(event){
      if (!event.target.classList.contains('menu') &&
        !event.target.closest('.menu') &&  !event.target.closest('.hamburger')){
        this.openMenu = false
      }
    },
    closeMenuByEscape(event){
      if(event.key === "Escape") {
        this.openMenu = false
      }
    },
    closeNoticeByClick(event){
      if (!event.target.classList.contains('notice') &&
        !event.target.closest('.notice') &&  !event.target.closest('.header-notice')){
        this.openNotice = false
      }
    },
    closeNoticeByEscape(event){
      if(event.key === "Escape") {
        this.openNotice = false
      }
    },
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
    document.body.addEventListener('click', this.closeNoticeByClick, false);
    document.addEventListener('keydown', this.closeNoticeByEscape, false);
  }
};
</script>

<style lang="scss">
@import '@/styles/variables.scss';

.page-header {
  background-color: #fff;
  box-shadow: 0px 1px 3px rgba(0, 0, 0, 0.2);
  &--auth {
    .header-container{
      justify-content: center;
    }
  }
}
.header-container{
  min-width: $mobile;
  display: flex;
  align-items: center;
  justify-content: space-between;
  min-height: 56px;
}
.header{
  height: 56px;
  background: #fff;
  position: relative;
  display:flex;
  justify-content: flex-end;
  align-items: center;
  box-shadow: 0px 1px 3px rgba(0, 0, 0, 0.2);
  min-width: 320px;
  @media(min-width:$tablet){
    background: #5461DC;
    box-shadow: 0px 1px 3px rgba(0, 0, 0, 0.2);
  }
    &-menu{
      background: #5461DC;
      width: 56px;
      height: 100%;
      position: absolute;
      left: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      @media(min-width:$tablet){
        border-right: 1px solid rgba(250, 250, 250, 0.5);
      }
    }
  &-account{
    width: 56px;
    display: flex;
    justify-content: center;
    align-items: center;
    border-left: 1px solid #F5F5F5;
    height: 100%;
    color: #6F6F6F;
    fill: #6F6F6F;
    @media(min-width:$tablet){
      border-left: 1px solid rgba(250, 250, 250, 0.5);
      color: #fff;
      fill:#fff;
    }
    @media(min-width:$desktop){
      width: auto;
      border: none;
    }
  }
  &-notice{
    width: 56px;
    display: flex;
    justify-content: center;
    align-items: center;
    border-left: 1px solid #F5F5F5;
    height: 100%;
    color: #6F6F6F;
    fill: #6F6F6F;
    position: relative;
    @media(min-width:$tablet){
      border-left: 1px solid rgba(250, 250, 250, 0.5);
      color: #fff;
      fill:#fff;
      order: 2;
    }
  }
  &-title{
    display:none;
    @media(min-width:$desktop){
      display: block;
      font-size: 14px;
      line-height: 20px;
      margin-right: 16px;
      margin-left: 7px;
      span{
        display: block;
        font-size: 10px;
        line-height: 16px;
        letter-spacing: 0.7px;
      }
    }
  }
}
.logo{
  display: none;
  @media(min-width:$tablet){
    display:block;
    position: absolute;
    left: 70px;
  }
}
.menu{
  width:56px;
  background: #1E1F23;
  position: absolute;
  left: 0;
  top: 56px;
  bottom:0;
  height:calc(100% - 56px);
  z-index:999;
  &-link{
    width: 56px;
    height: 56px;
    display: flex;
    align-items: center;
    justify-content: center;
    transition: background .3s;
    &:hover{
      background: #5461DC;
    }
    &.nuxt-link-active{
      background: #5461DC;
    }
  }
}
.slide-fade-enter-active {
  transition: all .3s ease;
}
.slide-fade-leave-active {
  transition: all .8s cubic-bezier(1.0, 0.5, 0.8, 1.0);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active до версии 2.1.8 */ {
  transform: translateX(10px);
  opacity: 0;
}
.notice-link{
  color: #6F6F6F;
  fill: #6F6F6F;
  @media(min-width: $tablet){
    color: #fff;
    fill: #fff;
  }
}
</style>

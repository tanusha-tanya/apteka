<template>
  <div id="my-appealse">
    <div class="container">
      <h1>Мои обращения</h1>
      <Mypagination/>
      <div class="flex">
        <Mysearch/>
        <Myaddbutton/>
      </div>
        <div class="message-header">
          <div class="message-number">№</div>
          <div class="message-date">Дата изменения</div>
          <div class="message-topic">Тема</div>
          <div class="message-name">Заголовок обращения</div>
          <div class="message-status">Статус сообщения</div>
          <div class="message-documents">Документы</div>
        </div>
        <Mymessage :status="'ready'" :date="'25 Октября 2018'" :topic="'Ошибка обмена'" :number="'10 387'" :title="'При обмене ошибка № 204040'" :documents="15"/>
        <Mymessage :status="'wait'" :date="'25 Октября 2018'" :topic="'Ошибка обмена'" :number="'10 387'" :title="'При обмене ошибка № 204040'" :documents="15"/>
        <Mymessage :status="'done'" :date="'26 Октября 2018'" :topic="'Запрос на изменение ИНН, наименования организации'" :number="'10 387'" :title="'Заменить название на «ООО “Аптека”»'" :documents="15"/>
    </div>
  </div>
</template>
<script>
  import Mypagination from '@/components/Mypagination'
  import Mysearch from '@/components/Mysearch'
  import Myaddbutton from '@/components/Myaddbutton'
  import Mymessage from '@/components/Mymessage'
  export default{
    components:{
      Mypagination,
      Mysearch,
      Myaddbutton,
      Mymessage
    }
  }
</script>
<style lang="scss">
  @import '@/styles/variables.scss';
  .flex{
    display: flex;
    justify-content: space-between;
    align-content: center;
    @media(min-width:$tablet){
      justify-content: flex-start;
    }
  }
  .message-header{
    display: none;
    @media(min-width:$desktop){
      display: flex;
      background: #fff;
      border-bottom: 1px solid #EAEAEA;
      margin: 0 -22px 0 -78px;
      padding: 20px 16px;
      padding-left: 78px;
      font-size: 12px;
      letter-spacing: 0.004em;
      color: #616161;
    }
  }
</style>
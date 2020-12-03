<template>
    <div id="topalert" class="topalert" v-if="openTopalert">
        <svg-icon name="info" width="24" height="24" class="topalert-icon" />
        <div class="topalert-text">            
            Внимание! Приложение partner.melzdrav.ru c 10.09.2019 в 18:00 (Мск) будет доступно по новому адресу partner-apteka.ru с сохранением данных
        </div>
        <a href="#" class="topalert-close" @click="openTopalert = false">
            <svg-icon name="cross" width="14" height="14" />
        </a>
    </div>
</template>
<script>
    export default{
        data(){
            return{
                openTopalert: true
            }
        },

    }
</script>
<style  lang="scss">
    @import '@/styles/variables.scss';
    .topalert{
        background: #FFC814;
        padding: 10px 16px;
        display: flex;
        justify-content: space-between;
        align-items: flex-start;
        font-size: 14px;
        line-height: 20px;
        color: #1E1F23;
        position: relative;
        @media(min-width: $tablet){
            align-items: center;
        }
        @media(min-width: $desktop){
            justify-content: flex-start;
        }
        &-icon{
            width: 24px;
            margin-right: 16px;
            margin-top: 5px;
            flex-shrink: 0;
            @media(min-width: $tablet){
                margin-top: 0;
            }
            @media(min-width: $desktop){
                margin-left: 18px;
                margin-right: 16px;
            }
        }
        &-close{
            margin-left:10px;
            margin-top: 5px;
            opacity: 0.5;
            @media(min-width: $tablet){
                margin-top: 0;
            }
            @media(min-width: $desktop){
                position: absolute;
                right: 16px;
                top: 15px;
            }
        }
    }
</style>
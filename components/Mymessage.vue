<template>
    <div id="message" class="message" :class="`message__${status}`">
        <Fullmessage v-if="fullMessage" @close="closeMessage"/>
        <a href="#" class="message-link" @click="fullMessage=true">
            <div class="message-title" :class="`message-title__${status}`">
                {{title}}
                <svg-icon name="triangle" width="5" height="10" />
            </div>
        </a>    
        <div class="message-body" @click="fullMessage=true">
            <div class="message-row message-status">
                <div class="message-value">
                    Статус:
                </div>
                <div class="message-info">
                    <div class="message-ready message-status" v-if="status=='ready'">
                        <svg-icon name="ready" width="14" height="12" />
                        Ответ получен
                    </div>
                    <div class="message-wait message-status" v-if="status=='wait'">
                        <svg-icon name="wait" width="14" height="14" /> 
                        Жду ответ
                    </div>
                    <div class="message-done message-status" v-if="status=='done'">
                        <svg-icon name="done" width="14" height="14" /> 
                        Выполненно
                    </div>
                </div>
            </div>
            <div class="message-row message-date">
                <div class="message-value">
                    Дата изменения:
                </div>
                <div class="message-info">
                    {{date}}
                </div>
            </div>
            <div class="message-row message-topic">
                <div class="message-value">
                    Тема:
                </div>
                <div class="message-info">
                    {{topic}}
                </div>
            </div>
            <div class="message-row message-number">
                <div class="message-value">
                    № обращения:
                </div>
                <div class="message-info">
                    {{number}}
                </div>
            </div>
            <div class="message-row message-row__big message-documents">
                <div class="message-info">
                    <svg-icon name="docs" width="16" height="16" class="message-doc" />
                    {{documents}}
                </div>    
            </div>
            <div class="message-row message-row__big message-name">
                <div class="message-info">
                    {{title}}
                </div>    
            </div>
        </div>
    </div>
</template>
<script>
    import Fullmessage from '@/components/Fullmessage'
    export default{
        name: 'mymessage',
        props:['status', 'date', 'topic', 'number', 'title', 'documents'],
        components:{
            Fullmessage
        },
        data(){
            return{
                fullMessage: false,
            }
        },
        methods:{
            closeMessage(){
                this.fullMessage = false
            }
        }
    }

</script>
<style lang="scss">
    @import '@/styles/variables.scss';
    .message{
        box-shadow: 0px 1px 3px rgba(0, 0, 0, 0.2);
        border-radius: 4px;
        margin: 8px 0;
        font-family: 'RobotoCondensed', sans-serif;         
        @media(min-width: $tablet){
            width: 624px;
        }
        @media(min-width:$desktop){
            width: auto;
            display: flex;
            box-shadow: none;
            background: #fff;
            border-radius: 0;
            border-bottom: 1px solid #EAEAEA;
            margin: 0 -22px 0 -78px;
            padding: 16px;
            padding-left: 78px;
        }
        &-link{
            display: block;
            @media(min-width:$desktop){
                display: none;
            }
        }  
        &-title{
            padding: 17px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            svg{
                color: #6F6F6F;
                fill: #6F6F6F;
            }
            &__ready{
                background: #fff;
                color: #1E1F23;
                font-size: 14px;
                font-weight: bold;
            }
            &__wait{
                background: #F5F5F5;
                color: #1E1F23;
                font-size: 14px;
                font-weight: normal;
            }
            &__done{
                color: #6F6F6F;
            }
        } 
        &-body{
            padding: 12px;
            padding-top: 8px;
            @media(min-width:$tablet){
                padding-top: 12px;        
            }
            @media(min-width:$desktop){
                display: flex;
                padding: 8px 0;
            }
        }
        &-row{
            display: flex;
            margin-bottom:10px;
            @media(min-width:$tablet){
                margin-bottom: 20px;
            }
            @media(min-width:$desktop){
                margin-bottom:0;
            }
            &__big{
                display:none;
                @media(min-width:$desktop){
                    display: flex;
                }
            }
        }
        &-value{
            font-size: 12px;
            letter-spacing: 0.004em;
            color: #6F6F6F;
            width: calc(50% - 15px);
            margin-right: 15px;
            @media(min-width:$tablet){
                width: 130px;
                margin-right: 39px;
                width: 110px;
                text-align: right;
            }
            @media(min-width:$desktop){
                display: none;
            }
        }
        &-info{
            font-size: 12px;
            letter-spacing: 0.004em;
            color: #1E1F23;
            width: 50%;
            @media(min-width:$tablet){
               font-size: 14px;
               width: auto;
            }
        }
        &-ready{
            color: #35AA67;
            svg{
                vertical-align: top;
                margin-right: 4px;
            }
        }
        &-wait{
            color: #FFC814;
             svg{
                vertical-align: top;
                margin-right: 4px;
            }
        }
        &-done{
            color: #6F6F6F;
            svg{
                vertical-align: top;
                margin-right: 4px;
            }
        }
        &-doc{
            vertical-align: top;
            color:  #1E1F23;
            fill:  #1E1F23;
        }
        &__done{
            color: #6F6F6F;
            .message-value, .message-info{
                color: #6F6F6F;
            }
            .message-doc{
                color: #6F6F6F;
            }
        }
        &__ready{
            @media(min-width:$desktop){
                font-family: 'RobotoCondensedBold', sans-serif;
            }
        }
        &__wait{
            @media(min-width:$desktop){
                background: #F5F5F5;
            }
        }
        &-number{
            @media(min-width:$desktop){
                order: 1;
                width: 100px;
                margin-right: 20px;
            }
        }
        &-date{
            @media(min-width:$desktop){
                order: 2;
                width: 140px;
                margin-right: 20px;
            }
        }
        &-topic{
            @media(min-width:$desktop){
                order: 3;
                width: 230px;
                margin-right: 20px;
            }
        }
        &-name{
            @media(min-width:$desktop){
                order: 4;
                width: 300px;
                margin-right: 20px;
            }
        }
        &-status{
            @media(min-width:$desktop){
                order: 5;
                width: 180px;
                margin-right: 20px;
            }
        }
        &-documents{
            @media(min-width:$desktop){
                order: 6;
                width: 100px;
                margin-right: 20px;
            }
        }
    }
</style>
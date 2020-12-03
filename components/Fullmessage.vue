<template>
    <div class="fullmessage">
        <div class="fullmessage-title">
            Просмотр обращения №234
            <a href="#" class="fullmessage-cross"  @click.prevent="close">
                <svg-icon name="cross" width="16" height="16" />
            </a>
        </div>
        <div class="fullmessage-date">
            29 марта 2018 в 21:56
        </div>
        <div class="fullmessage-body">
            <div class="fullmessage-top">
                <span class="fullmessage-row">
                    <label class="fullmessage-label">Тема</label>
                    <div class="fullmessage-select"> Ошибка обмена  
                        <svg-icon name="select" width="12" height="7" class="fullmessage-arrow"/>
                    </div>
                </span>
                <span class="fullmessage-row">
                    <label class="fullmessage-label">Заголовок обращения</label>
                    <div class="fullmessage-select"> Не работает обмен с аптекой
                    </div>
                </span>  
            </div>
            <div class="fullmessage-content">
                <vuescroll :ops="ops">
                    <div class="fullmessage-answer fullmessage-answer__my">
                        <div class="fullmessage-name">ООО «Системы автоматизации»</div>
                        <div class="fullmessage-message"> Сообщение с описанием проблемы </div>
                        <div class="fullmessage-day">30.11.18 12:34</div>
                    </div>
                    <div class="fullmessage-answer fullmessage-answer__support">
                        <div class="fullmessage-name">Служба тех. поддержки</div>
                        <div class="fullmessage-message">Примечание, чтобы отправить свой шаблон напрямую в запросе, используйте  параметры html и text;
                            Второй вариант отправки сообщения - использовать параметр template для отправки статичного шаблона, загруженный ранее в сервис и передавать только значения к переменным (заданным ранее в шаблоне) через параметр  
                        </div>
                        <div class="fullmessage-day">30.11.18 12:34</div>
                    </div>
                </vuescroll>
            </div>
            <div class="fullmessage-bottom">                    
                <p class="fullmessage-send">Для отправки напишите сообщение</p>
                <span class="fullmessage-row">
                    <span class="fullmessage-flex">
                        <label for="adddocument">
                            <svg-icon name="docs" width="11" height="22" class="fullmessage-doc" />
                        </label>
                        <input type="file" class="fullmessage-file" id="adddocument">                            
                        <input type="text" placeholder="Напишите сообщение..." class="fullmessage-text">
                        </span>
                    </span>
                    <span class="fullmessage-bordered">
                        <button type="button" class="cansel" @click.prevent="close">Отменить</button>
                        <button type="submit" class="send" @click.prevent="myerror">Отправить</button>
                    </span>
                </div>    
        </div>
    </div>
</template>
<script>
    import Multiselect from 'vue-multiselect'
    import resolveError from "@/helpers/resolveError"
    import vuescroll from 'vuescroll'
    export default{
         components: {
            Multiselect,
            vuescroll
        },
        data(){
            return{
                options: ['Ошибка обмена', 'Запрос на изменение ИНН, наименования организации'],
                value: 'Выберите тему',
                ops: {
                    vuescroll: {},
                    scrollPanel: {},
                    rail: {},
                    bar: {
                        background: '#1E1F23',
                        opacity: 0.4,
                        KeepShow: true
                    }
                },
            }
        },
        methods:{
            close(){
                this.$emit('close')
            },         
            closeAlertByEscape(event){
                if(event.key === "Escape" || event.key === "Enter") {            
                   this.close()                   
                }                 
            }    
        },
    }
</script>
<style lang="scss">
    @import '@/styles/variables.scss';
    .fullmessage{
        background: #fff;
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        height: 568px;
        width: 100%;
        font-family: 'RobotoRegular', sans-serif;
        @media(min-width:$tablet){
            left: 56px;
            width: calc(100% - 56px);
        }
        @media(min-width:$desktop){
            left: auto;
            right: 0;
            width: 648px;
            height: 720px;
            z-index: 997;
        }
        &-title{
            background:#FAFAFA;
            padding: 16px;
            position: relative;
            font-size: 16px;
            letter-spacing: 0.0015em;
            color: #1E1F23;
            display: flex;
            justify-content: space-between;
            align-items: center;
            height: 48px;
            box-sizing: border-box;
            height: 56px;
            font-family: 'RobotoBold', sans-serif;
            @media(min-width: $tablet){
                height: 56px;
                font-size: 24px;
                letter-spacing: 0.25px;
            }
        }
        &-date{
            background: #F2F2F2;
            color: #616161;
            padding: 5px 16px;
            letter-spacing: 0.004em;
            font-size: 12px;
        }
        &-select{
            font-size: 14px;
            background: #FAFAFA;
            border: 2px solid #EAEAEA;
            height: 48px;
            box-sizing: border-box;
            padding: 14px 16px;
            color: #1E1F23;
            font-family: Roboto, sans-serif;
            position: relative;
            font-weight: 300;
            border-radius: 4px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        &-name{
            font-size: 12px;
            letter-spacing: 0.004em;
            color: #1E1F23;
            font-family: 'RobotoBold', sans-serif;
            margin-bottom: 4px;
            @media(min-width:$tablet){
                font-size: 14px;
            }
        }
        &-day{
            color: #999999;
            letter-spacing: 0.7px;
            font-size: 10px;
            text-align: right;
        }
        &-message{
            font-size: 12px;
            letter-spacing: 0.004em;
            color: #1E1F23;
            line-height: 16px;
            @media(min-width:$tablet){
                font-size: 14px;
                line-height: 20px;
                order: 2;
                width: 100%;
            }            
        }
        &-input{
            font-size: 14px;
            background: #FAFAFA;
            border: 2px solid #EAEAEA;
            padding: 14px 16px;
            width: 100%;
            height: 48px;
            box-sizing: border-box;
        }
        &-label{
            font-size: 12px;
            letter-spacing: 0.004em;
            color: #616161;
            margin-bottom: 8px;
        }
        &-top{
           padding: 7px 18px;  
           border-bottom: 2px solid #EAEAEA;           
        }
        &-row{
            margin: 11px 0;
            display: block;
        }
        &-form{
            display: flex;
            height: calc(100vh - 50px);
            flex-direction: column;
            justify-content: space-between;
        }
        &-bottom{
            background: #F5F5F5;
            padding: 12px 16px;
        }
        &-send{
            color: #1E1F23;
            letter-spacing: 0.004em;
            font-size: 12px;
            @media(min-width: $tablet){
                font-size: 14px;
            }
        }
        &-flex{
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        &-file{
            position: absolute;
            visibility: hidden;
        }
        &-text{
            width: 256px;
            height: 48px;
            padding: 16px;
            box-sizing: border-box;
            border: none;
            outline:none;
            @media(min-width: $tablet){
                width: 632px;
                margin-right: 8px;
            }
            @media(min-width: $desktop){
                width: 576px;
            }
        }
        &-bordered{
            margin: 0 -16px;
            border-top: 2px solid #EAEAEA;
            display: flex;
            justify-content: flex-end;
            padding:21px 40px;
        }
        &-content{
            overflow: hidden;
            height: 207px;
            background: #fff;
            .__view{
                display: flex;
                flex-direction: column;
                justify-content: flex-end;
            }
            @media(min-width:$tablet){
                height: 256px;
                display: flex;
                flex-direction:column;
                align-items: flex-end;
            }
        }
        &-answer{
            margin: 0 31px 8px 16px;
            border: 1px solid #F5F5F5;
            padding: 12px 8px 8px 12px;
            border-radius: 4px;
            &__support{
                background: #FFFCEB;
                margin: 0 16px 8px 31px;
            } 
            @media(min-width: $tablet){
                padding: 16px;
                display: flex;
                flex-wrap: wrap;
                justify-content: space-between;
            }           
        }
    }  
    .cansel{
        letter-spacing: 0.75px;
        font-size: 14px;
        text-transform: uppercase;
        color: #616161;
        width: 108px;
        height: 40px;
        display: flex;
        justify-content: center;
        align-content: center;
        border: 1px solid #EAEAEA;
        background: #fff;
        border-radius: 50px;
        margin-right: 16px;
    }
    .send{
        letter-spacing: 0.75px;
        font-size: 14px;
        text-transform: uppercase;
        color: #616161;
        width: 132px;
        height: 40px;
        display: flex;
        justify-content: center;
        align-content: center;
        border: 1px solid #EAEAEA;
        background: #fff;
        border-radius: 50px;
        background: #DADADA;
        opacity: 0.3;
    }  
</style>
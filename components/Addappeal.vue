<template>
    <div class="addappeal">
        <div class="addappeal-title">
            Добавить обращение
            <a href="#" class="addappeal-cross"  @click.prevent="close">
                <svg-icon name="cross" width="16" height="16" />
            </a>
        </div>
        <div class="addappeal-body">
            <form class="addappeal-form">
                <div class="addappeal-top">
                    <span class="addappeal-row">
                        <label class="addappeal-label">Тема</label>
                        <Multiselect
                            class="addappeal-select"
                            :options="options"
                            :placeholder="value"
                        />
                    </span>
                    <span class="addappeal-row">
                        <label class="addappeal-label">Заголовок обращения</label>
                        <input type="text" class="addappeal-input" >
                    </span>  
                </div>
                <div class="addappeal-bottom">                    
                    <p class="addappeal-send">Для отправки напишите сообщение</p>
                    <span class="addappeal-row">
                        <span class="addappeal-flex">
                            <label for="adddocument">
                                <svg-icon name="docs" width="11" height="22" class="addappeal-doc" />
                            </label>
                            <input type="file" class="addappeal-file" id="adddocument">                            
                            <input type="text" placeholder="Напишите сообщение..." class="addappeal-text">
                        </span>
                    </span>
                    <span class="addappeal-bordered">
                        <button type="button" class="cansel" @click.prevent="close">Отменить</button>
                        <button type="submit" class="send" @click.prevent="myerror">Отправить</button>
                    </span>
                </div>    
            </form>
        </div>
    </div>
</template>
<script>
    import Multiselect from 'vue-multiselect'
    import resolveError from "@/helpers/resolveError";

    export default{
         components: {
            Multiselect
        },
        data(){
            return{
                options: ['Ошибка обмена', 'Запрос на изменение ИНН, наименования организации'],
                value: 'Выберите тему',
            }
        },
        methods:{
            close(){
                this.$emit('close')
            },
            myerror(){
                this.$emit('myerror')
            },           
           closeAlertByEscape(event){
                if(event.key === "Escape" || event.key === "Enter") {            
                   this.close()                   
                }                 
            }    
        },
    }
</script>
<style lang="scss" scoped>
    @import '@/styles/variables.scss';
    .addappeal{
        background: #fff;
        position: absolute;
        top: 0;
        left: 0;
        right: 0;
        height: 568px;
        width: 100%;
        z-index: 997;
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
            @media(min-width: $tablet){
                height: 56px;
                font-size: 24px;
                letter-spacing: 0.25px;
            }
        }
        &-select{
            .multiselect__tags{
                font-size: 14px;
                background: #FAFAFA;
                border: 2px solid #EAEAEA;
                height: 48px;
                box-sizing: border-box;
                border-radius: 4px;
            }
            .multiselect__single, .multiselect__input{
                background: #FAFAFA;
            }
            .multiselect__option--highlight{
                background: #5461DC;
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
            border-radius: 4px;
        }
        &-label{
            font-size: 12px;
            letter-spacing: 0.004em;
            color: #616161;
            margin-bottom: 8px;
        }
        &-top{
           padding: 7px 18px;             
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
            display: none;
            @media(min-width:$tablet){
                margin: 0 -16px;
                border-top: 2px solid #EAEAEA;
                display: flex;
                justify-content: flex-end;
                padding:21px 40px;
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
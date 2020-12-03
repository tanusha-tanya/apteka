<template>    
    <div class="adderror">
        <div class="adderror-head">
            Загрузить файл 
            <a href="#" class="adderror-cross"  @click.prevent="close">
                <svg-icon name="cross" width="16" height="16" />
            </a>
        </div>
        <div class="adderror-content">  
            <div class="adderror-title">
                Файл должен быть
            </div>
            <ul class="adderror-ul">
                <li class="adderror-li">Вес файла не должен привышать 10Мб</li>
                <li class="adderror-li">Файл должен быть в формате pdf, jpg, png, xlsx, docx, csv</li>
            </ul>
            <label for="adderror-file" class="adderror-label">Выбрать файл</label>
            <input type="file" id="adderror-file" placeholder="Выбрать файл" class="adderror-file">
        </div>
        <div class="adderror-bottom">  
            <a href="#" class="adderror-cansel" @click.prevent="close">  Отмена</a>
        </div>
   </div>
</template>

<script>
    export default {
        name: 'Adderror',
        props: {       
            title: String,
            content: String,
            link: String,            
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
        mounted(){
            let alertWrapper = document.createElement('div');
            alertWrapper.className = 'alertwrapper';           
            alertWrapper.style.height=document.body.clientHeight + "px";
            document.body.append(alertWrapper);
            alertWrapper.addEventListener('click', this.close, false);  
            document.addEventListener('keydown', this.closeAlertByEscape, false);       
        },   
        destroyed(){
            let alertWrapper = document.querySelector('.alertwrapper');
            alertWrapper.remove();    
            document.removeEventListener('keydown', this.closeAlertByEscape, false);        
        }   
    }
</script> 
<style lang="scss">
@import '@/styles/variables.scss';
    .adderror{
        background: #FFF;
        z-index: 999;
        position: fixed;
        width:100%;
        left:0;
        top: 100px;        
        box-sizing: border-box;
        box-shadow: 0px 8px 10px rgba(0, 0, 0, 0.2), 0px 6px 30px rgba(0, 0, 0, 0.12), 0px 16px 24px rgba(0, 0, 0, 0.14);
        border-radius: 4px;
        @media(min-width:$tablet){
            width: 496px;
            left: calc(50% - 248px);
        }
        &-head{
            font-size: 16px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: #FAFAFA;
            padding: 16px;
            @media(min-width:$tablet){
                font-size: 24px;
                letter-spacing: 0.25px;
            }
        }
        &-content{
            padding: 16px;
        }
        &-title{
            font-size: 14px;
            font-weight: 700;
            color: #1E1F23;
        }
        &-ul{
            padding: 0;
            margin: 18px 0;
        }
        &-li{
            font-size: 14px;
            color: #1E1F23;
            padding-left:19px;
            margin: 8px 0;
            position: relative;
            &:before{
                content: '';
                width: 2px;
                height: 2px;
                display: block;
                background:  #6F6F6F;
                position: absolute;
                left: 9px;
                top: 5px;
            }
        }
        &-file{
            position: absolute;
            visibility: hidden;
        }
        &-label{
            margin: 40px auto 32px auto;
            position: relative;
            display: flex;
            justify-content: center;
            align-items: center;
            background: #5461DC;
            border-radius: 200px;
            letter-spacing: 0.004em;
            font-size: 12px;
            color: #fff;
            width: 160px;
            height: 40px;
        }
        &-bottom{
            border-top: 2px solid #EAEAEA;
            padding: 16px;
            display: flex;
            justify-content: flex-end;
        }
        &-cansel{
            letter-spacing: 0.004em;
            color: #616161;
            font-size: 12px;
            border: 1px solid #EAEAEA;
            border-radius: 50px;
            width: 104px;
            height: 40px;
            display: flex;
            justify-content: center;
            align-items: center;
        }
    }
    .alertwrapper{
        position: absolute;
        width: 100%;
        height: 100%;
        top:0;
        bottom: 0;
        left: 0;
        right:0;
        background:#000000;
        opacity: 0.32;
        z-index: 998;
    }
</style>
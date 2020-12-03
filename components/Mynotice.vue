<template>
    <div id="notice" class="notice">
        <vuescroll :ops="ops">
            <div class="notice-title">Уведомления</div>
            <div class="notice-row" v-for="info in 5">
                <div class="notice-date">20.05.2019</div>
                <div class="notice-info">Получен ответ на обращение №345</div>
            </div>
        </vuescroll>
    </div>
</template>
<script>
    import vuescroll from 'vuescroll';
    export default{
        components: {
            vuescroll
        },
        data(){
            return {
                ops: {
                    vuescroll: {},
                    scrollPanel: {},
                    rail: {},
                    bar: {
                        background: '#1E1F23',
                        opacity: 0.4,
                        KeepShow: true
                    }
                }
            }
        }
    }
</script>
<style lang="scss">
    @import '@/styles/variables.scss';
    .notice{
        position: absolute;
        z-index: 999;
        background: #fff;
        width: 288px;
        box-shadow: 0px 5px 6px rgba(0, 0, 0, 0.2), 0px 3px 16px rgba(0, 0, 0, 0.12), 0px 9px 12px rgba(0, 0, 0, 0.14);
        border-radius: 4px;
        top: 14px;
        right: -39px;        
        box-sizing: border-box;
        height: 320px;
        overflow: hidden;
        @media(min-width: $tablet){
            right: 22px;
            width: 280px;
        }
        @media(min-width: $desktop){
            right:9px;
            top: 8px;
        }
        &-title{
            background: #FAFAFA;
            padding: 10px 16px;
            color: #616161;
            font-size: 14px;
        }
        &-row{
            border-bottom: 1px solid #EAEAEA;
            padding: 10px 16px;
            padding-bottom: 20px;
        }
        &-date{
            font-size: 10px;
            letter-spacing: 1.5px;
            line-height: 16px;
        }
        &-info{
            font-size: 14px;
            line-height: 20px;
            color: #1E1F23;
        }
    }
</style>
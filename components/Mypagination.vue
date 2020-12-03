<template>
    <div class="pagination-wrap"> 
        <Addappeal @close="closeAdd" @myerror="openError" v-if="addIsOpen"/>
        <Adderror @close="closeerror" v-if="errorisOpen"/>
        <div class="pagination">
            <div class="pagination-content">
                <div class="pagination-counter">
                    1-50 из 695
                </div>
                <div class="pagination-arrow pagination-arrow__prev">
                    <a href="#" class="pagination-prev">
                        <svg-icon name="arrow" width="7" height="12" />
                    </a>
                </div>
                <a class="pagination-num pagination-num__current" href="#">1</a>
                <a class="pagination-num" href="#">2</a>
                <a class="pagination-num" href="#">3</a>
                <a class="pagination-num" href="#">4</a>
                <a class="pagination-num pagination-num__small" href="#">5</a>
                <a class="pagination-num pagination-num__small" href="#">6</a>
                <a class="pagination-num pagination-num__small" href="#">7</a>
                <a class="pagination-etc">...</a>
                <a class="pagination-num pagination-num__big" href="#">36</a>
                <a class="pagination-num pagination-num__big" href="#">37</a>
                <a class="pagination-num pagination-num__big" href="#">38</a>
                <a class="pagination-num pagination-num__big" href="#">39</a>
                <a class="pagination-num pagination-num__big" href="#">40</a>
                <a class="pagination-num pagination-num__large" href="#">41</a>
                <a class="pagination-num pagination-num__large" href="#">42</a>
                <div class="pagination-arrow pagination-arrow__next">
                    <a href="#" class="pagination-next">
                        <svg-icon name="arrow" width="7" height="12" />
                    </a>
                </div>
            </div>
            <a href="#" class="pagination-link" @click.prevent="addIsOpen=true"> Добавить </a>
        </div>
    </div>
</template>
<script>
    import Addappeal from '@/components/Addappeal'
    import Adderror from '@/components/Adderror'
    export default{
        name: 'myaddbutton',
        components:{
            Addappeal,
            Adderror
        },
        data(){
            return{
                addIsOpen: false,
                errorisOpen: false
            }
        },
        methods:{
            closeAdd(){
                return this.addIsOpen = false
            },
            openError(){
                this.errorisOpen = true
            },
            closeerror(){
                this.errorisOpen = false
            }
        }
    }
</script>
<style lang="scss">
    @import '@/styles/variables.scss';
    .pagination{
        margin: 10px -16px 15px -16px;
        height: 46px;
        background: #fff;
        border-top: 1px solid #EAEAEA;
        border-bottom: 1px solid #EAEAEA;
        padding: 10px 16px;
        padding-left: 16px;  
        position: relative;      
        @media(min-width:$tablet){
            margin: 8px -22px 16px -78px;
            padding-left: 78px;
            height: 50px;
        }
        @media(min-width:$desktop){
            height: 57px;
            border-top: none;
            margin-bottom: 0;
        }
        &-content{
            display: flex;
            justify-content: space-between;
            box-sizing: border-box;
            @media(min-width:$desktop){
                width: 50%;
            }
        }
        &-num{
            font-size: 12px;
            line-height: 16px;
            color: #6F6F6F;
            width: 24px;
            height: 24px;
            border-radius: 100%;
            background: #F2F2F2;
            display: flex;
            justify-content: center;
            align-items: center;
            transition: background .3s;
            border: 1px solid #EAEAEA;
            @media(min-width:$tablet){
                background: none;
                border: none;
                width: 32px;
                height: 32px;
                font-size: 14px;
            }
            &__current, &:hover{
                background:#5461DC;
                color: #fff;
                @media(min-width:$tablet){
                    border: 1px solid #EAEAEA;
                    background: #F2F2F2;
                    color: #5461DC;
                }
            }
            &__big{
                display: none;
                @media(min-width:$tablet){
                    display: flex;
                }
                @media(min-width:$desktop){
                    display: none;
                }
            }
            &__small{
                @media(min-width:$tablet){
                    display: none;
                }                
            }
            &__large{
               display: none;
                @media(min-width:$tablet){
                    display: flex;
                } 
            }
        }
        &-etc{
            align-self:flex-end;
        }
        &-arrow{
            &__prev{
                border-right: 2px solid #EAEAEA;
                padding-right: 10px;
                display: flex;
                justify-content: center;
                align-items: center;
                @media(min-width:$tablet){
                    order: 2;
                    border-right: none;
                    border-left: 2px solid #EAEAEA;
                    padding-left: 20px;
                }
            }
            &__next{
                border-left: 2px solid #EAEAEA;
                padding-left: 10px;
                display: flex;
                justify-content: center;
                align-items: center;
                @media(min-width:$tablet){
                    order: 3;
                    border: none;
                }
                svg{
                    transform: rotate(180deg)
                }
            }
        }
        &-counter{
            display:none;
            @media(min-width:$tablet){
                display: block;
                font-size: 12px;
                padding-right: 14px;
                padding-top: 10px;
                color: #616161;
                border-right: 2px solid #EAEAEA;
                letter-spacing: 0.004em;
            }
        }
        &-link{
            display: none;
            @media(min-width:$desktop){
                position: absolute;
                box-sizing: border-box;
                display: flex;
                align-items: center;
                justify-content: center;
                right: 16px;
                top: 8px;
                width: 118px;
                height: 40px;
                background: #5461DC;
                color: #fff;
                border-radius: 200px;
                font-size: 14px;
                text-align: center;
                letter-spacing: 0.75px;
                text-transform: uppercase;
            }
        }
    }
</style>
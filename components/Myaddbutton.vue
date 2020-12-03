<template>
  <div id="addbutton">
    <a href="#" class="addbutton-link" @click.prevent="addIsOpen = true">
        <svg-icon name="add" width="24" height="24"/>
    </a>
    <Addappeal @close="closeAdd" @myerror="openError" v-if="addIsOpen"/>
    <Adderror @close="closeerror" v-if="errorisOpen"/>
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
    .addbutton-link{
        display: flex;
        justify-content: center;
        align-items: center;
        width: 40px;
        height: 40px;
        background:#5461DC;
        border-radius: 5px;
        @media(min-width:$tablet){
            width: 48px;
            height: 48px;
            margin-left: 15px;
        }
        @media(min-width:$desktop){
            display: none;
        }
    }
</style>
<template>    
    <div id="search">
        <label for="searchappeal" class="search-label">
            <svg-icon name="search" width="17" height="17" class="search-svg"/>
            <input type="search" class="search" id="searchappeal" placeholder="Поиск">
        </label>
    </div>
</template>
<script>
    export default{
        name: 'mysearch'
    }
</script>
<style lang="scss">
    @import '@/styles/variables.scss';
    #search{
        @media(min-width: $desktop){
            display: none;
        }
    }
    .search{
        width: 240px;
        height: 40px;
        border: 1px solid #EAEAEA;
        box-sizing: border-box;
        background: #FAFAFA;
        padding-left: 40px;
        padding-right: 16px;
        border-radius: 5px;
        @media(min-width: $tablet){
            width: 561px;
            height: 48px;
        }
        &-label{
            position: relative;
            display: block;
        }
        &-svg{
            position: absolute;
            left: 12px;
            top: 12px;
            @media(min-width: $tablet){
                top: 16px;
            }
        }
    }
</style>
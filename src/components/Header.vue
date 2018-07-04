<template>
    <header>
         <img src="/static/img/logo.svg" alt="Helios Marvel API">
    </header>
</template>

<script>
export default {
    
}
</script>

<style lang="postcss" scoped>
    header{
        height: 60px;
        display: flex;
        align-items: center;
        justify-content: center;
        border-bottom: 1px solid #ebebeb;
        background-color: #fff;
        position:fixed;
        width: 100%;
        z-index: 10;
    }
    header img{
        height: 28px;
    }
    @media(orientation:landscape){
        header{
            height: 45px;
        }
    }
    @media (min-width: 768px){
        header{
            height: 60px;
        }
    }
</style>



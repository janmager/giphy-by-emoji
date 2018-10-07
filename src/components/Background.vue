<template>
    <div class="background">
    
    </div>
</template>

<script>
export default {
    name: 'Background'
}
</script>

<style lang="scss" scoped>
    .background{
        position: fixed;
        width: 100%;
        height: 100vh;
        top: 0;
        z-index: -1;
        background-image: url('../assets/bg.jpg');
        background-repeat: no-repeat;
        background-size: cover;
        background-position: 50% 0%;
    } 
    .background:after{
        content: '';
        background: rgba(0,0,0,.6);
        position: absolute;
        top: 0;
        left: 0;
        z-index: 1;
        width: 100%;
        height: 100vh;
    }
</style>

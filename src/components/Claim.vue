<template>
    <div class="claimWrapper">
        <h1 class="claim">GIPHY-by-EMOJI</h1>
        <!-- <p class="subclaim">
            Find gif on gifpy.com based on entered emoji.
            <br><br>
            Tap word to see recomended emojis.
        </p> -->
    </div>
</template>

<script>
    export default {
        name: 'Claim',
    }
</script>

<style lang="scss" scoped>
    .claimWrapper{
        display: flex;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        color: white;
    }
    .claim{
        font-size: 50px;
        margin: 0;
        font-weight: 800;

        @media (min-width: 768px){
            font-size: 70px;
        }

        @media (min-width: 1024px){
            font-size: 100px;
        }
        
    }
    .subclaim{
        margin: 50px 0 0 0;
        font-size: 13px;
        font-weight: 400px;
        line-height: 125%;
        max-width: 500px;

        @media (min-width: 768px){
            font-size: 14px;
        }

        @media (min-width: 1024px){
            font-size: 16px;
        }
    }
</style>

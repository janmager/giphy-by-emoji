<template>
    <div class="blackBg" />
</template>

<script>
export default {
    name: 'Backdrop',
}
</script>

<style lang="scss" scoped>
    .blackBg{
        min-width: 100%;
        min-height: 100%;
        background: rgba(0,0,0,0.6);
        position: fixed;
        top: 0;
        left: 0;
        z-index: 998;
    }
</style>

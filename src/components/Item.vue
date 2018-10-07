<template>
    <div class="item">
        <img :src="gif">
    </div>
</template>

<script>
export default {
    name: 'Item',
    props: {
        item: {
            type: Object,
            required: true,
        },
    },
    data(){
        return{
            // photo: this.item.links[0].href,
            // title: this.item.data[0].title,
            gif: this.item.images.downsized.url,
        };
    },
    computed: {
        // style(){
        //     return `backgroundImage: url("${this.photo}")`;
        // }
    }
};
</script>

<style land="scss" scoped>
    .item{
        width: 250px;
        height: 250px;
        background-size: cover;
        background-repeat: no-repeat;
        background-position: 50%;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .item img{
            max-width: 100%;
            max-height: 100%;
        }
</style>

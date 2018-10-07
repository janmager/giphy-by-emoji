<template>
    <div class="outerWrapper">
        <div class="innerWrapper">
            <div class="photo">
                <img :src="photo">
            </div>
            <div class="description">
                <h2 class="title">{{ title }}</h2>
                <p class="description">
                    {{ desc }}
                </p>
            </div>
        </div>
        <div class="close" @click="$emit('closeModal')"/>
    </div>
</template>

<script>
export default {
    name: 'Modal',
    props: {
        item: {
            type: Object, 
            required: true
        }
    },
    data(){
        return{
            photo: null,
            title: null,
            desc: null,
        };
    },
    mounted() {
        this.photo = this.item.links[0].href;
        this.title = this.item.data[0].title;
        this.desc = this.item.data[0].description.substring(0,200);
    }
}
</script>

<style lang="scss" scoped§>
    .outerWrapper{
        background: #f6f6f6;
        height: auto;
        width: 100%;
        max-width: 600px;
        position: fixed;
        top: 50%;
        left: 50%;
        z-index: 999;
        transform: translate(-50%, -50%);
        box-shadow: 0 30px 30px rgba(0,0,0,.4);

        @media(max-width: 786px){
            height: 100%;
            width: 100%;
            max-width: 100%;
            top: 0;
            left: 0;
            transform: translate(0,0);
            box-shadow: 0px;
        }
    }
    .close{
        position: absolute;
        right: 0px;
        top: 0px;
        padding: 15px;
        width: 30px;
        height: 30px;
        cursor: pointer;

        &::before,
        &::after{
            position: absolute;
            content: '';
            width: 20px;
            height: 2px;
            top: 20px;
            right: 20px;
            background: black;
            display: block;
        }

        &::before{
            transform: rotate(45deg)
        }

        &::after{
            transform: rotate(-45deg)
        }
    }
    .innerWrapper{
        display: flex;
        height: 100%;
        padding: 50px;
        justify-content: center;
        align-items: center;
        flex-direction: column;
        .photo{
            width: 100%;
            height: auto;

            img{
                width: 100%;
                max-width: 400px;
                max-height: 400px;
            }
        }
        .description{
            color: #333;
        }
        h2{
            font-weight: 800;
            font-size: 32px;
            margin-top: 20px;
        }
        p{
            margin-top: 20px;
            line-height: 150%;
        }
    }
</style>

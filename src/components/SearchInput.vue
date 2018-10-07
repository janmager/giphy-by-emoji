<template>
    <input 
        id="search" 
        name="search"
        :value="value"
        :class="{ dark }"
        @input="handleChange"
        placeholder="Sad face"
        autofocus
    />
</template>

<script>
export default {
    name: 'SearchInput',
    props: {
        value: {
            type: String,
            required: true,
        },
        dark: {
            type: Boolean,
            default: false,
        }
    },
    methods: {
        handleChange(e){
            this.$emit('input', e.target.value);
        },
    },
}
</script>

<style lang="scss" scoped> 
    input{
            margin-top: 50px;
            display: flex;
            color: white;
            text-align: center;
            font-size: 26px;
            font-family: Montserrat, sans-serif;    
            height: 30px;
            border: 0;
            background: rgba(0,0,0,.3);
            border: 2px solid white;
            padding: 30px;
            transition: box-shadow ease-out .3s;

            @media (min-width: 1024px){
                font-weight: 400px;
            }
    }

    input::placeholder{
        color: rgb(155, 155, 155);
    }

    input:focus{
        outline: none;
        box-shadow:0px 0px 15px rgba(255,255,255,0.6);
    }

    .dark{
        border-bottom-color: black;
        color: black;
    }

    .dark:focus{
        outline: none;
        box-shadow: 0 10px 20px -8px rgba(0,0,0,0.2);
    }
</style>

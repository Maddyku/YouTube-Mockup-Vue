<template>
    <div>   
        <input @input="onInput" />
    </div>
</template>


<script>
export default {
    name: 'SearchBar',
    methods: {  //Ability to manipulate state inside of application
        //Event Handler onInput
        onInput: function(event) {
//communicate from child to parent (down-up) by emitting events
            this.$emit('onInputChange', event.target.value);
        }
    }
}
</script>

<style scoped>
    input {
        width: 75%
    }

    div {
        text-align: center;
        margin: 20px;
    }
</style>
<template>
    <button @mousedown="$emit('btn-rapid-plus')" mouseleave="$emit('clear')" @mouseup="$emit('clear')"  id="plus" class="clockBtn" :style="{pointerEvents: isDisabled}">
        <i id="plus" class="fas fa-plus clockBtn"></i>
    </button>
    <button @mousedown="$emit('btn-rapid-minus')" @mouseleave="$emit('clear')" @mouseup="$emit('clear')"  id="minus" class="clockBtn" :style="{pointerEvents: isDisabled}">
        <i id="minus" class="fas fa-minus clockBtn"></i>
    </button>
</template>


<script>
    export default {
        name: 'Button',
        emits : ['btn-rapid-plus', 'btn-rapid-minus', 'clear'],
        props: {
            isDisabled: String
        }
    }
</script>


<style scoped>
    .clockBtn {
        padding: 4px 5px;
        font-size: 15px;
        background: #464646;
        color: #fff;
        border: none;
        margin: 0 2px;
    }

    .clockBtn:focus {
        outline: none;
    }
</style>
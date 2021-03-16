<template>
    <div class="g__cell" @click="move(indexCell)">
        {{value !== 0 ? value : ""}}
    </div>
</template>

<script>
    export default {
        name: "Cell",
        props: {
            indexCell: {
                type: Number,
                default: 0
            },
            value: {
                type: Number,
                default: 0
            }
        },
        methods: {
            move(indexCell) {
                this.$emit('move', indexCell)
            }
        }
    }
</script>

<style lang="scss" scoped>
    .g {
        &__cell {
            position: relative;
            display: flex;
            justify-content: center;
            align-items: center;
            width: 100px;
            height: 100px;
            border: 1px solid #e7e7e7;
            border-radius: 5px;
            font-size: 56px;
            background: #fff;
            color: #000;
            cursor: pointer;
        }
    }
</style>
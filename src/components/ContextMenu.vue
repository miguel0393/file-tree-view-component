<template>
    <div v-if="show" :style="{ 'top': yPosition + 'px', 'left': xPosition + 'px'}" class="custom-cm"
        @contextmenu="(e) => e.preventDefault()"
    > 
        <div class="custom-cm__item">Item #1</div>
        <div class="custom-cm__item">Item #2</div>
        <div class="custom-cm__item">Item #3</div>
        <div class="custom-cm__divider"></div>
        <div class="custom-cm__item">Item #4</div>
    </div>
</template>

<script>
export default {
    name: "ContextMenu",
    props: {
        xPosition: {
            type: Number,
            default: 0
        },
        yPosition: {
            type: Number,
            default: 0
        },
        show: {
            type: Boolean,
            default: false
        }
    }
}
</script>

<style scoped>

    .custom-cm {
        text-align: left;
        color: black;
        background-color: aliceblue;
        border: 1px solid #cccccc;
        box-shadow: 1px 1px 10px rgb(0, 0, 0, 0.1);
        padding: 10px 0px;
        position: absolute;
        width: 200px;
    }

    .custom-cm__item {
        cursor: pointer;
        padding: 8px 15px;
    }

    .custom-cm__item:hover {
        background-color: antiquewhite;
    }

    .custom-cm__divider {
        border-bottom: 1px solid #eeeeee;
        margin: 10px 0px;
    }

</style>
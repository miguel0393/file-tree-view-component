<template>
    <div id="app" class="custom-cm"
        v-if="visible"
        :style="{ 'top': yPosition + 'px', 'left': xPosition + 'px'}" 
        @contextmenu="(e) => e.preventDefault()"
    > 
        <div id="cn" class="custom-cm__item" @click="optionClicked">Cambiar Nombre</div>
        <div id="ac" class="custom-cm__item" @click="optionClicked">Agregar Carpeta</div>
        <div id="aa" class="custom-cm__item" @click="optionClicked">Agregar Archivo</div>
    </div>
    
</template>

<script>
export default {
    name: "ContextMenu",
    props: {
        visible: {
            type: Boolean,
            default: false
        },
        xPosition: {
            type: Number,
            default: 0
        },
        yPosition: {
            type: Number,
            default: 0
        }        
    },
    methods: {
        optionClicked() {
            this.visible = false;
            this.$emit("onClick");
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
</style>
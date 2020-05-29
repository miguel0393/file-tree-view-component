<template>
    <div id="app" class="custom-cm"
        v-if="visible"
        :style="{ 'top': yPosition + 'px', 'left': xPosition + 'px'}" 
        @contextmenu="(e) => e.preventDefault()"
    > 
        <div class="custom-cm__item" @click="changeName">Cambiar Nombre</div>
        <div class="custom-cm__item" @click="addFolder">Agregar Carpeta</div>
        <div class="custom-cm__item" @click="addFile">Agregar Archivo</div>
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
        changeName() {
            this.visible = false;
            this.$emit("onClick", "Cambiar Nombre", "Ingrese el nombre del elemento");
        },
        addFolder() {
            this.visible = false;
            this.$emit("onClick", "Agregar Carpeta", "Ingrese el nombre del elemento");
        },
        addFile() {
            this.visible = false;
            this.$emit("onClick", "Agregar Archivo", "Ingrese el nombre del elemento");
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
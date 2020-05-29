<template>
    <div id="app">
        <transition name="fade" appear> 
        <div class="modal" v-if="visible">
            <h1>{{title}}</h1>
            <p>{{description}}</p>
            <input type="text">
            <button @click="buttonClicked">Ok</button>
            <button @click="buttonClicked">Cancel</button>
        </div>
        </transition> 
    </div>
</template>

<script>
export default {
    name: "ModalDialog",
    props: {
        title: String,
        description: String,
        visible: {
            type: Boolean,
            default: false
        }
    },
    methods: {
        buttonClicked() {
            this.visible = false;
             this.$emit("onClick");
        }
    }
}
</script>

<style scoped>

    .modal {
        position: fixed;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        z-index: 99;

        width: 100%;
        max-width: 400px;
        background-color: #FFF;
        color: black;
        border-radius: 16px;
        padding: 25px;
    }

    .modal h1 {
            color: #222;
            font-size: 23px;
            font-weight: 900;
            margin-bottom: 15px;
    }

    .modal p {
            color: #666;
            font-size: 18px;
            font-weight: 400;
            margin-bottom: 15px;
    }

    .modal input[type=text] {
        width: 100%;
        padding: .5rem;
    }

    .modal button {
        width: 30%;
        margin: 15px;
        padding: .5rem;
    }

</style>
<template>
    <div id="app">
        <transition name="fade" appear> 
        <div class="modal" v-if="visible">
            <h1>MODAL DIALOG</h1>
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Provident quos libero corrupti a porro pariatur unde, nesciunt, atque esse suscipit quas explicabo? Modi similique nobis obcaecati provident hic ut aut!</p>
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
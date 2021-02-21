<template>
    <div class="navigation max-w-full w-full flex items-center p-4 m-4 bg-gray-800 text-orange-300 rounded-lg min-w-0">
        <subnav button-name="Home"/>
        <subnav button-name="Post"/>
        <subnav button-name="Edit"/>
        <subnav button-name="Delete"/>
        <subnav button-name="Test"/>
        <modal v-if="showModal" @close="onClick(false)">
            <h1 slot="header">Title</h1>
        </modal>
        <img src="../assets/mail.png" class="w-1/6 invisible sm:w-1/6 sm:visible"/>
    </div>
</template>

<script>
    import modal from './modal.vue'
    import subnav from './subnav.vue'
    import { EventBus } from './event-bus.js'
    export default {
        props: [],
        components: { subnav, modal },
        data() {
            return {
                showModal: false,
                state: false
            }
        },
        methods: {
            onClick(state) {
                EventBus.$emit('modal', state);
            }
        },
        mounted() {
            EventBus.$on("Post", (state) => { this.showModal = state});
            EventBus.$on("Close", (state) => { this.showModal = state});
             if(this.state == true) {
                 this.showModal = true;
             }
        }
    };
</script>

<style scoped>
    .navigation {
    /* display: flex; */
    /* flex-direction: row;
    justify-content: center; */
    /* width: auto;
    height: auto; */
    /* flex-basis: 100%; */

    /* text-align: center; */

    /* margin: 10px;
    padding: 10px; */

    /* background-color: #3c2f56; */
    /* color: #e58a7a; */
    
    /* font-size: 15px; */
    font-family: Arial, Helvetica, sans-serif;
    
    /* border-radius: 5px; */
}
</style>
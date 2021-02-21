<template>
    <div class="subnav hover:bg-gray-600 rounded-lg screen:min-w-0">
        <div class="lg:text-4xl sm:text-xs lg:m-4 sm:m-0.8" @click="onClick(buttonName)">
            {{buttonName}}
        </div>
    </div>
</template>

<script>
    import { EventBus } from './event-bus.js';
    //import navigation from './navigation.vue'
    export default {
        props: ['buttonName'],
        data() {
            return {
                action: "",
                message: ""
            }
        },
        methods: {
            onClick(name){
                this.action = name;
                EventBus.$emit(`${this.action}`, `empty`);
            }
        }
    };
</script>

<style scoped>
    .subnav {
        /* width: auto;
        height: auto; */

        /* margin-left: 10px;
        margin-right: 10px; */
        margin: 0 auto;
        
        align-self: center;
        cursor: default;
        
        /* border-radius: 3px; */
        /* border: 3px solid red; */
    }
</style>
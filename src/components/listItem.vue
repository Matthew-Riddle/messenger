<template>
    <draggable tag="ul" ghost-class="moving-card" filter=".action-button" class="w-full" :list="notes" :animation="200">
        <li v-for="note in notes" 
        :key="note.id"
        :note="note"
        @click="note.show = !note.show"
        class="p-4 mb-3 flex items-center bg-white shadow rounded-lg cursor-move">
            {{note.title}}
            <transition name="slide-fade">
                <p class="p-4 m-4 items-center justify-center bg-gray-600" v-if="note.show">{{note.message}}</p>
            </transition>
        </li>
        
    </draggable>
</template>

<script>
import draggable from "vuedraggable"
import { EventBus } from "./event-bus.js"

export default {
    props: [  ],
    components: { draggable },
    data() {
        return {
            count: 0,
            notes: []
        }
    },
    mounted() {
        EventBus.$on("PostOk", (message) => { this.onClick("Post", message) });
        EventBus.$on("Delete", () => { this.onClick("Delete") });
        EventBus.$on("textData", (note) => { this.notes.push(note)})
    },
    
    methods: {
        onClick(action, message) {
            var vm = this;

            // var openmodal = document.querySelectorAll('.')

            if(action === "Post") {
                vm.count += 1;
                console.log('Post', vm.count);
                console.log(message.title);
                vm.notes.push({id:vm.count, title: message.title, message: message.note, show: false})
            }
            if(action === "Delete") {
                if(vm.count != 0) {
                    vm.count -= 1;
                    console.log('Delete', vm.count);
                    vm.notes.pop()
                }
            }
        }
        // Fill this in with what we want to happen. Modal pops up when we click post, send that form info over on the event bus and use it here in this method
    }
}

// function onClick() {
//     this.notes.push({title: "new buddy", message: "Hello there friend!"})
// }
// EventBus.$on("Post", () => {this.methods.onClick()});
</script>

<style>
    .slide-fade-enter-active {
        transition: all .3s ease;
    }
    .slide-fade-leave-active {
        transition: all .3s cubic-bezier(1.0, 0.5, 0.8, 1.0);
    }
    .slide-fade-enter, .slide-fade-leave-to {
        transform: translateX(10px);
        opacity: 0;
    }
</style>
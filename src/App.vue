<template>
  <div id="app" class="min-h-screen w-screen max-w-full bg-gray-900 flex flex-col items-center p-4">
    <navigation></navigation>
    <list></list>
  </div>
</template>

<script>
import './assets/css/tailwind.css'
import navigation from './components/navigation.vue'
import list from './components/listItem.vue'
//import { EventBus } from './components/event-bus.js'

// EventBus.$on("Post", () => { list.methods.onClick() });
export default {
  components: { navigation, list },
  data() {
    return {
      showModal: false
    }
  }
}
</script>

<style>
  #show-modal {
    background: chartreuse;
  }
</style>

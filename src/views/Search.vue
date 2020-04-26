<template>
  <div id="app">
    <form>
    <h1>{{ message }}</h1>
    <input v-model="message">
    <button @click="warn(message, $event)">
      Submit
    </button>
    </form>
  </div>
</template>

<script>
  //import SearchForm from "@/components/SearchForm.vue"
  export default {
    name: 'app',
    data: () => ({
      message: 'ceci est un message'
    }),
    methods: {
      warn: function (message, event) {
        // now we have access to the native event
        if (event) {
          event.preventDefault()
        }
        alert(message)
      }
    }
  }
  

</script>
  

<style>

</style>
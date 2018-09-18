<template>
  <div id="app">
    <Editor v-model="msg"/>
    <button class="btn" @click="submitContent">Отправить</button>
    
    <div class="messages">
      <div class="message"
           v-for="(message, i) in messages"
           :key="i"
           v-html="message"
           @click="onEdit(i)"
      ></div>
    </div>
    
  </div>
</template>

<script>
  import { Vue, Component } from "vue-property-decorator";
  import Editor from "./components/Editor.vue";

  @Component({
    components: {
      Editor
    }
  })
  export default class App extends Vue {
    msg = "";
    messages = [];

    submitContent () {
      this.messages.push(this.msg);
      this.msg = "";
    }

    onEdit (i) {
      this.msg = this.messages[i];
    }
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  .messages {
    width: 500px;
    margin: 50px auto;
  }

  .message {
    border: 1px solid red;
    margin-bottom: 20px;
    padding: 20px;
    cursor: pointer;
  }
</style>

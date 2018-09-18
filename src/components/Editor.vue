<template>
  <div class="editor">
    <div class="toolbar">
      <button class="btn"
              v-for="button in buttons"
              v-html="button.html"
              @click="makeStyle(button.style)"
      ></button>
    </div>
    <div class="content"
         id="content"
         contenteditable="true"
         @input="$emit('input', $event.target.innerHTML)"
         ref="content"
    ></div>
  </div>
</template>

<script>
  import { Vue, Component, Prop, Watch } from "vue-property-decorator";

  @Component({
    props: {
      value: String
    }
  })
  export default class Editor extends Vue {
    buttons = [
      {style: "bold", html: "<b>Ж</b>"},
      {style: "underline", html: "_"},
      {style: "italic", html: "<i>K</i>"}
    ];

    makeStyle (style) {
      document.execCommand(style);
    }

    @Watch("value")
    onValueChanged (val) {
      if (this.$refs.content.innerHTML !== val)
        this.$refs.content.innerHTML = val;
    }
  }
</script>

<style lang="scss">
  .editor {
    width: 500px;
    margin: 0 auto;
    border: 1px solid black;
    .toolbar {
      border-bottom: 1px solid black;
    }
    .content {
      min-height: 100px;
      text-align: left;
      &:focus {
        outline: none;
      }
    }
    .footer {
      text-align: right;
    }
  }
</style>
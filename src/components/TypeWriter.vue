<template>
  <div class="ce-typewriter">
    <div
      class="typewriter"
      :style="styling"
    >
      <p
        class="typewriter__text"
        :style="textStyle"
        v-html="typeWriterValue"
      ></p>
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      text: {
        type: String,
        default: "Question everything,<br> defy the status quo<br>Punk's Not Dead:<br>A DIY Survival Guide",
      },
      speed: {
        type: Number,
        default: 100,
      },
      backgroundColor: {
        type: String,
        default: "#ffffff",
      },
      textColor: {
        type: String,
        default: "#000000",
      },
      textAlign: {
        type: String,
        default: "left",
      },
      fontSize: {
        type: String,
        default: "max(24px, 32px)",
      },
      fontFamily: {
        type: String,
        default: "impact_labelregular, 'courier new', monospace",
      },
      fontWeight: {
        type: String,
        default: "400",
      },
      lineHeight: {
        type: String,
        default: "1.5",
      },
      letterSpacing: {
        type: String,
        default: "normal",
      },
      padding: {
        type: String,
        default: "0.125em 0.25em",
      },
    },
    name: "TypeWriter",
    version: "1.0.0",
    data() {
      return {
        typeWriterValue: "",
        charIndex: 0,
        textToType: this.text,
      };
    },
    computed: {
      styling() {
        return {
          fontSize: this.fontSize,
          fontFamily: this.fontFamily,
          fontWeight: this.fontWeight,
          textAlign: this.textAlign,
          lineHeight: this.lineHeight,
          padding: this.padding,
        };
      },
      textStyle() {
        return {
          display: "inline",
          color: this.textColor,
          boxDecorationBreak: "clone",
          WebkitBoxDecorationBreak: "clone",
          padding: "0.125em 0.25em",
          backgroundColor: this.backgroundColor,
          fontFamily: this.fontFamily,
          letterSpacing: this.letterSpacing,
        };
      },
    },
    watch: {
      text: {
        immediate: true,
        handler(newText) {
          this.resetTypewriter(newText);
        },
      },
      charIndex() {
        this.type();
      },
    },
    methods: {
      type() {
        if (this.charIndex < this.textToType.length) {
          setTimeout(() => {
            this.typeWriterValue += this.textToType.charAt(this.charIndex);
            this.charIndex += 1;
          }, this.speed);
        }
      },
      resetTypewriter(newText) {
        this.typeWriterValue = "";
        this.charIndex = 0;
        this.textToType = newText;
        this.type();
      },
    },
    mounted() {
      this.type();
    },
  };
</script>
<style scoped>
  /* @import "_impact-label.css"; */
  @font-face {
    font-family: "impact_labelregular";
    src: url("./assets/fonts/Impact_Label-webfont.woff") format("woff");
    font-weight: normal;
    font-style: normal;
    font-display: swap;
  }
</style>

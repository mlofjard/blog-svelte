<script lang="ts">
  import { Highlight, HighlightAuto } from "svelte-highlight";
  import xml from "svelte-highlight/languages/xml";
  import javascript from "svelte-highlight/languages/javascript";
  import css from "svelte-highlight/languages/css";
  import bash from "svelte-highlight/languages/bash";
 // import typescript from "svelte-highlight/languages/typescript";
  import atomOneDark from "svelte-highlight/styles/atom-one-dark";

  export let lang: string;
  export let text: string;

  const getLanguage = (lang: string) => {
    switch(lang) {
      case "html": return xml;
      case "bash": return bash;
      case "css": return css;
      case "js": return javascript;
   //   case "typescript": return typescript;
      default: return bash;
    }
  }

  $: language = getLanguage(lang);
</script>

<!-- <pre class={lang}><code>{text}</code></pre> -->

<svelte:head>
  {@html atomOneDark}
</svelte:head>

<Highlight {language} code={text} />

<style lang="scss">
  :global(pre) {
    font-family: "Inconsolata", monospace;
    margin-bottom: 1.6rem;
    white-space: pre-wrap;
  }
</style>
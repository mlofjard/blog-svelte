<script>
  export let raw
</script>

<code>{raw.replace(/`/g, '')}</code>

<style lang="scss">
  @import "../../../styles/variables.scss";

  code {
    background-color: $color-light-gray;
    border: 1px solid $color-gray;
    font-family: "Inconsolata", monospace;
    padding: 0 .2rem;
  }
</style>

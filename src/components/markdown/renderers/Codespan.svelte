<script>
  export let raw
</script>

<code>{raw.replace(/`/g, '')}</code>

<style lang="scss">
  @import "../../../styles/variables.scss";

  code {
    font-family: "Fira Code", monospace;
    font-weight: 400;
  }
</style>

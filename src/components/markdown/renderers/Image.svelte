<script>
   export let href = "";
   export let title = undefined;
   export let text = "";
</script>

<img src={href} {title} alt={text} />

<style>
   img {
      width: 100%;
      max-width: 49rem;
   }
</style>

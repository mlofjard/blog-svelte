<script>
  export let href = ''
  export let title = undefined
</script>

<a {href} {title}><slot></slot></a>

<style>
  a {
    color: rgb(0,180,180);
  }
</style>

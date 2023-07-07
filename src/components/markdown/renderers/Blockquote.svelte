<blockquote><slot /></blockquote>

<style lang="scss">
    @use "../../../styles/variables.scss" as *;

   blockquote {
    quotes: auto;
    position: relative;
    padding-left: 2.4rem;
    margin-bottom: 1.6rem;
    font-style: italic;

      &::before {
         content: open-quote;
         position: absolute;
         left: 0;
         font-size: 4rem;
         margin-top: -1.6rem;
         color: $color-accent;
      }

      &::after {
        content: no-close-quote;
      }
   }
</style>

<script lang="ts">
   export let dialog: HTMLDialogElement;
   export let url: string;

   const close = (e: MouseEvent) => {
      e.preventDefault();
      dialog.close();
   };

   const copy = (e: MouseEvent) => {
      e.preventDefault();
      navigator.clipboard.writeText(url).then(
         () => {
            dialog.close();
         },
         () => {
            console.error("Could not copy URL to clipboard.", url);
         }
      );
   };
</script>

<dialog bind:this={dialog}>
   <p>Sorry, sharing is not available as a feature in your browser.</p>
   <p>You can share the link to the page if you want!</p>
   <code>{url}</code>
   <div class="buttons">
      <button on:click={copy}>Copy to clipboard</button><button on:click={close}>Close</button>
   </div>
</dialog>

<style lang="scss">
   dialog {
      padding: 2.4rem 2.4rem 3.2rem 2.4rem;
      font-size: 1.6rem;
      color: rgb(225, 225, 225);
      background-color: rgba(40, 40, 40, 1);
      filter: drop-shadow(0 0.2rem 0.2rem rgba(0, 0, 0, 0.4));
      border: none;
      border-radius: 1.6rem;
      text-align: center;

      code {
         padding: 0.4rem;
         border: 1px solid rgb(180, 180, 180);
         font-family: "Inconsolata";
         font-weight: 400;
         background: rgb(80, 80, 80);
         display: block;
         margin-bottom: 2.4rem;
         margin-top: 1.6rem;
         word-break: break-all;
      }

      .buttons {
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        gap: .8rem;
        justify-content: center;
      }

      button {
         background: rgb(205, 205, 205);
         color: rgb(40, 40, 40);
         border: none;
         padding: 0.8rem 2.4rem;
         border-radius: 1.6rem;
         font-family: "Oswald", sans-serif;
         font-size: 1.6rem;

         &:hover,
         &:focus {
            background: rgb(225, 225, 225);
         }
      }

      &::backdrop {
         background-color: rgba(0, 0, 0, 0.6);
      }

      p {
         margin-bottom: 0.8rem;
      }
   }
</style>

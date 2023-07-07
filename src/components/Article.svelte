<script lang="ts">
   import { link } from "svelte-navigator";
   import { prettyDate } from "../utils";
   import type { Article } from "types/articles";
   import Markdown from "./markdown/Markdown.svelte";
   import ShareDialog from "./ShareDialog.svelte";

   export let item: Article;
   export let titleLink: boolean = false;

   let dialog: HTMLDialogElement;

   const getTheme = (theme: string) => {
      if (theme === "code" || theme === "life" || theme === "fun") {
         return theme;
      }
      return "life";
   };

   const share = (e: MouseEvent) => {
      e.preventDefault();
      if (navigator.share) {
         navigator
            .share({
               title: document.title,
               text: item.value.title,
               url: fullUrl,
            })
            .then(() => console.log("Successful share"))
            .catch(error => console.log("Error sharing:", error));
      } else {
         dialog.showModal();
      }
   };

   $: theme = getTheme(item.value.theme);
   $: postUrl = `/post/${item.value.readableKey}`;
   $: fullUrl = `${window.location.origin}${postUrl}`;
</script>

<article class={theme}>
   <header>
      <time datetime="item.value.dateTime">{prettyDate(item.value.dateTime)}</time>
      {#if titleLink}
         <h1><a href={postUrl} use:link>{item.value.title}</a></h1>
      {:else}
         <h1>{item.value.title}</h1>
      {/if}
   </header>
   <div class="wrapper">
      <div class="content">
         <Markdown source={item.value.htmlContent} {theme} />
         <footer>by {item.value.author}</footer>
      </div>
      <aside>
         <a href="{postUrl}#comments" class="commentcount"><span class="symbols">chat</span></a>
         <a href="#" on:click={share} class="commentcount"><span class="symbols">share</span></a>
      </aside>
   </div>
   <ShareDialog bind:dialog url={fullUrl} />
</article>

<style lang="scss">
   @import "../styles/variables.scss";

   article {
      display: flex;
      flex-direction: column;
      max-width: 120rem;
      width: 100%;

      header {
         padding: 0 0 0.8rem 1.6rem;
         filter: drop-shadow(0 0.2rem 0.2rem rgba(0, 0, 0, 0.4));

         h1 {
            margin: 0;
            font-family: "Oswald", sans-serif;
            font-size: 4.8rem;
            color: rgba(205, 205, 205, 1);
            text-transform: uppercase;

            &::first-letter {
               font-size: 120%;
            }

            a {
               text-decoration: none;
               color: inherit;

               &:hover {
                  text-decoration: underline;
               }
            }
         }
      }

      footer,
      header time {
         color: rgba(225, 225, 225, 1);
         font-size: 1.2rem;
         font-style: italic;
         font-weight: 600;
      }

      footer {
         text-align: right;
      }

      .wrapper {
         display: flex;
         flex-direction: row;

         .content {
            flex: 1 1 100%;
            background: rgba(40, 40, 40, 0.8);
            filter: drop-shadow(0 0.2rem 0.2rem rgba(0, 0, 0, 0.4));
            padding: 1.6rem 1.6rem 2.4rem 1.6rem;
            border-radius: 1.6rem;
            color: rgba(225, 225, 225, 1);
            line-height: 1.6;
            font-size: 1.6rem;
         }

         aside {
            flex: 1 0 fit-content;
            margin: 0.8rem 0 0 0.8rem;
            gap: 0.8rem;
            display: flex;
            flex-direction: column;

            a {
               display: block;
               text-decoration: none;
               color: rgba(225, 225, 225, 1);
               filter: drop-shadow(0 0.2rem 0.2rem rgba(0, 0, 0, 0.4));

               span.symbols {
                  font-size: 4rem;
               }
            }
         }
      }

      .symbols {
         font-family: "Material Symbols Rounded";
         font-feature-settings: "liga";
         font-weight: normal;
         font-style: normal;
         font-size: 2.4rem;
         display: inline-block;
         line-height: 1;
         text-transform: none;
         letter-spacing: normal;
         word-wrap: normal;
         white-space: nowrap;
         direction: ltr;
         -webkit-font-feature-settings: "liga";
         -webkit-font-smoothing: antialiased;
      }

      @container (max-width: 450px) {
         .wrapper {
            flex-direction: column;

            aside {
               flex-direction: row;

               a span.symbols {
                  font-size: 4rem;
               }
            }
         }
      }
   }
   // article {
   //    box-shadow: 0 3px 16px -2px rgba(0, 0, 0, 0.1);
   //    max-width: 80rem;
   //    padding: 0.8rem 1.6rem 2.4rem 1.6rem;
   //    color: $color-dark;
   //    border-radius: 0.8rem;
   //    line-height: 1.5;
   //    border-top: 0.4rem solid #000000;
   //    border-bottom: 0.4rem solid #000000;

   //    > h1 {
   //       font-size: 1.6rem;
   //       text-transform: uppercase;
   //       font-weight: 600;
   //       margin-bottom: 0.8rem;

   //       &::first-letter {
   //          color: #000000;
   //          font-size: 2.4rem;
   //       }

   //       > a {
   //          color: $color-dark;
   //          text-decoration: none;

   //          &:hover {
   //             border-bottom: 0.2rem solid $color-dark;
   //          }
   //       }
   //    }

   //    > div.time {
   //       font-style: italic;
   //    }

   //    &.code {
   //       border-color: $color-blue;
   //       > h1 {
   //          &::first-letter {
   //             color: $color-blue;
   //          }
   //       }
   //    }

   //    &.life {
   //       border-color: $color-yellow;
   //       > h1 {
   //          &::first-letter {
   //             color: $color-yellow;
   //          }
   //       }
   //    }

   //    &.fun {
   //       border-color: $color-red;
   //       > h1 {
   //          &::first-letter {
   //             color: $color-red;
   //          }
   //       }
   //    }
   // }
</style>

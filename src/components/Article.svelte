<script lang="ts">
    import { link } from "svelte-navigator";
    import { prettyDate } from "../utils";
    import type { Article } from "types/articles";
    import Markdown from "./markdown/Markdown.svelte";

    export let item: Article;
    export let titleLink: boolean = false;

    const getTheme = (theme: string) => {
        if (theme === "code" || theme === "life" || theme === "fun") {
            return theme;
        }
        return "life";
    };

    $: theme = getTheme(item.value.theme);
    $: postUrl = `/post/${item.value.readableKey}`;
</script>

<article class={theme}>
    <div class="time">{prettyDate(item.value.dateTime)}</div>
    {#if titleLink}
        <h1><a href={postUrl} use:link>{item.value.title}</a></h1>
    {:else}
        <h1>{item.value.title}</h1>
    {/if}
    <Markdown source={item.value.htmlContent} {theme} />
</article>

<style lang="scss">
    @import "../styles/variables.scss";

    article {
        box-shadow: 0 3px 16px -2px rgba(0, 0, 0, 0.1);
        max-width: 80rem;
        padding: 0.8rem 1.6rem 2.4rem 1.6rem;
        color: $color-dark;
        border-radius: 0.8rem;
        line-height: 1.5;
        border-top: 0.4rem solid #000000;
        border-bottom: 0.4rem solid #000000;

        > h1 {
            font-size: 1.6rem;
            text-transform: uppercase;
            font-weight: 600;
            margin-bottom: 0.8rem;

            &::first-letter {
                color: #000000;
                font-size: 2.4rem;
            }

            > a {
                color: $color-dark;
                text-decoration: none;

                &:hover {
                    border-bottom: 0.2rem solid $color-dark;
                }
            }
        }

        > div.time {
            font-style: italic;
        }

        &.code {
            border-color: $color-blue;
            > h1 {
                &::first-letter {
                    color: $color-blue;
                }
            }
        }

        &.life {
            border-color: $color-yellow;
            > h1 {
                &::first-letter {
                    color: $color-yellow;
                }
            }
        }

        &.fun {
            border-color: $color-red;
            > h1 {
                &::first-letter {
                    color: $color-red;
                }
            }
        }
    }
</style>

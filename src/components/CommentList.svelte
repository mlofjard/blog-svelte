<script lang="ts">
    import { prettyDate } from "../utils";
    import type { Comment } from "../../types/articles";

    export let comments: Comment[];
    export let theme: string;

    $: styles = `comments ${theme}`
</script>

<section class={styles}>
    {#each comments as comment}
        <div class="comment">
            <div class="author">by {comment.value.name} on {prettyDate(comment.value.dateTime)}</div>
            {comment.value.comment}
        </div>
    {/each}
    {#if comments.length == 0}
        <div class="nocomment">No comments yet... =(</div>
    {/if}
</section>

<style lang="scss">
    @import "../styles/variables.scss";

    section.comments {
        box-shadow: 0 3px 16px -2px rgba(0, 0, 0, 0.1);
        margin: 0 0;
        border-radius: 0.8rem;
        background-color: $color-white;
        border-top: 0.4rem solid #000;
        border-bottom: 0.4rem solid #000;
        overflow: hidden;

        &.code { border-color: $color-blue; }
        &.life { border-color: $color-yellow; }
        &.fun { border-color: $color-red; }

        .nocomment {
            padding: 0.8rem 1.6rem;
            font-style: italic;
        }

        .comment {
            padding: 0.8rem 1.6rem;
            &:nth-child(even) {
                background-color: $color-light-gray;
            }

            .author {
                font-size: .8rem;
                padding-bottom: .4rem;
                margin-bottom: .8rem;
                border-bottom: 1px solid $color-gray;
            }
        }
    }
</style>

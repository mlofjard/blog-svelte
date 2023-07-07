<script lang="ts">
    import { link } from "svelte-navigator";

    export let firstPage: boolean;
    export let lastPage: boolean;
    export let nextUrl: string;
    export let nextTitle: string;
    export let prevUrl: string;
    export let prevTitle: string;
</script>

<div class="container">
    {#if !firstPage}
        <a href={prevUrl} use:link>{prevTitle}</a>
    {/if}
    {#if !lastPage}
        <a href={nextUrl} use:link>{nextTitle}</a>
    {/if}
</div>

<style lang="scss">
    @use "../styles/variables.scss" as *;

    .container {
        max-width: 60rem;
        margin: 1.6rem auto;
        display: flex;
        flex-direction: row;
        justify-content: center;
        align-items: center;
        gap: 1.6rem;

        a {
            border-radius: 0.8rem;
            box-shadow: 0 3px 16px -2px rgba(0, 0, 0, 0.1);
            color: $color-dark;
            text-align: center;
            padding: .8rem 1.6rem .8rem 1.6rem;
            background-color: $color-white;
            font-size: .8rem;
            line-height: .8rem;
            font-weight: 600;
            text-decoration: none;
            text-transform: uppercase;
            flex: 0 1 12rem;
            transition: all 300ms ease-in-out,
                color 300ms ease-in-out;
            //border-left: 0.4rem solid $color-red;
            border: 0.2rem solid $color-blue;

            &::first-letter {
                font-size: 120%;
            }

            &:hover {
                border-width: .4rem;
                border-color: $color-red;
                margin: -.2rem -.2rem;
            }
        }
    }
</style>

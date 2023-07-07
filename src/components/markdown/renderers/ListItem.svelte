<script>
    export let ordered;
    export let theme;

    $: styles = ordered ? `ordered ${theme}` : `unordered ${theme}`;
</script>

<li class={styles}><slot /></li>

<style lang="scss">
    @use "../../../styles/variables.scss" as *;

    li.unordered {
        &::before {
            content: "\2022"; /* Add content: \2022 is the CSS Code/unicode for a bullet */
            color: $color-accent; /* Change the color */
            font-weight: bold; /* If you want it to be bold */
            display: inline-block; /* Needed to add space between the bullet and the text */
            width: 1em; /* Also needed for space (tweak if needed) */
            margin-left: -1em; /* Also needed for space (tweak if needed) */

        }
        // &.code::before {
        //     color: $color-blue;
        // }
        // &.life::before {
        //     color: $color-yellow;
        // }
        // &.fun::before {
        //     color: $color-red;
        // }
    }
</style>

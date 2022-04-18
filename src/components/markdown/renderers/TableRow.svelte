<script>
    export let header;
    export let theme;

    $: rowClass = header ? `header ${theme}` : `body ${theme}`;
</script>

<tr class={rowClass}><slot /></tr>

<style lang="scss">
    @import "../../../styles/variables.scss";

    tr.body {
        &:nth-child(even) {
            background-color: $color-light-gray;
        }

        &:last-of-type {
            border-bottom: 0.2rem solid #000;
        }
    }

    tr.body.code:last-of-type {
        border-bottom-color: $color-blue;
    }
    tr.body.life:last-of-type {
        border-bottom-color: $color-yellow;
    }
    tr.body.fun:last-of-type {
        border-bottom-color: $color-red;
    }
</style>

<script lang="ts">
    export let theme: string;
</script>

<thead class={theme}><slot /></thead>

<style lang="scss">
    @import "../../../styles/variables.scss";

    thead {
        font-weight: 600;
        background-color: $color-light-gray;
    }

    thead.code {
        background-color: $color-blue;
        color: $color-white;
    }
    
    thead.life {
        background-color: $color-yellow;
        color: $color-dark;
    }
    
    thead.fun {
        background-color: $color-red;
        color: $color-white;
    }
</style>

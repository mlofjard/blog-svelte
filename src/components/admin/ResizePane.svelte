<script lang="ts">
    const grabberWidth = 10;

    export let leftWidth = 60;
    export let middleWidth = 60;

    let leftPane;
    let middlePane;

    let expanding = "";
    let startLeft = 0,
        initialLeft = leftWidth,
        startMiddle = 0,
        initialMiddle = middleWidth;

    function startExpand(type: string, event: any) {
        expanding = type;
        if (type == "left") {
            startLeft = event.pageX;
            initialLeft = leftWidth;
            return;
        }
        if (type == "middle") {
            startMiddle = event.pageX;
            initialMiddle = middleWidth;
            return;
        }
    }

    function stopExpand() {
        expanding = "";
        startLeft = 0;
        startMiddle = 0;
        //initial = null
    }

    function expand(event: any) {
        if (!expanding) return;

        if (expanding == "left") {
            const delta = event.pageX - startLeft;
            leftWidth = initialLeft + delta;
            return;
        }

        if (expanding == "middle") {
            const delta = event.pageX - startMiddle;
            middleWidth = initialMiddle + delta;
            return;
        }
    }
</script>

<svelte:window on:mouseup={stopExpand} />
<div on:mousemove={expand} class="container">
    <section
        class="resizepane"
        style="max-width: {leftWidth}px;"
        bind:this={leftPane}
    >
        <slot name="left" />
    </section>
    <section
        class="resizepane"
        style="max-width: {middleWidth}px"
        bind:this={middlePane}
    >
        <div class="handle" on:mousedown={startExpand.bind(leftPane, "left")} />
        <slot name="middle" />
    </section>
    <section class="restpane">
        <div
            class="handle"
            on:mousedown={startExpand.bind(middlePane, "middle")}
        />
        <slot name="right" />
    </section>
</div>

<style lang="scss">
    .container {
        display: flex;
        flex-direction: row;
        flex: 1;
    }

    .resizepane {
        display: flex;
        flex-direction: row;
        //align-items: stretch;
        width: 100%;
        flex: 1 1 auto;
        overflow: auto;
    }

    .handle {
        background-color: grey;
        flex: 0 0 8px;
    }

    .restpane {
        display: flex;
        flex-direction: row;
        //align-items: stretch;
        width: 100%;
        flex: 1 1 auto;
        overflow: auto;
    }
</style>

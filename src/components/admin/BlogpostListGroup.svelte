<script lang="ts">
    import { link } from "svelte-navigator";

    interface Group {
        name: string;
        posts: {
            draft: boolean;
            dateTime: string;
            key: string;
            title: string;
        }[];
    }

    export let group: Group;

    let expanded = group.name === "Drafts" ? true : false;

    const toggle = () => {
        expanded = !expanded;
    };

    $: listStyles = expanded ? "postlist expanded" : "postlist";
    $: headerStyles = expanded ? "header expanded" : "header";
</script>

<div class="group">
    <button class={headerStyles} on:click={toggle}>
        <div class="name">{group.name}</div>
    </button>
    <div class={listStyles}>
        {#each group.posts as post}
            <div class="post">
                <a href="/admin/post/{post.key}" use:link>- {post.title}</a>
            </div>
        {/each}
    </div>
</div>

<style lang="scss">
    .group {
        border: 1px solid rgb(120,120,120);
        border-bottom: none;

        &:last-of-type {
            border-bottom: 1px solid rgb(120,120,120);
        }
    }

    .header {
        display: flex;
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        width: 100%;
        padding: 0.8rem;
        background: rgb(40,40,40);
        color: rgb(225,225,225);
        border: none;
        font-family: 'Oswald', sans-serif;
        font-size: 1.6rem;

        &:hover {
            background: rgb(50,50,50);
        }

        &::after {
            display: block;
            font-family: "Material Symbols Rounded";
            content: "\e5cf";
        }

        &.expanded {
            background: rgb(60,60,60);
            &::after {
                font-family: "Material Symbols Rounded";
                display: block;
                content: "\e5ce";
            }
        }
    }

    .postlist {
        display: none;
        padding-bottom: 1.6rem;
        background: rgb(60,60,60);

        &.expanded {
            display: block;
        }
    }
    .post {
        padding: 0 0 0 1.6rem;
        
        a {
            font-family: 'Open Sans', sans-serif;
            font-size: 1.6rem;
            width: 100%;
            color: rgb(225,225,225);
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
            text-decoration: none;
            line-height: 1.5;
            display: inline-block;
        }
    }
</style>

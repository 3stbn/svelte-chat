<script>
    import { Collection } from 'sveltefire'
    import { tick } from 'svelte'
    import AppendMessage from './AppendMessage.svelte'

    export let user
    let chatsElement

    async function scrollToTheEnd() {
        await tick()
        chatsElement.scrollTo(0, chatsElement.scrollHeight)
    }
</script>

<style>
    .is-sender {
        text-align: right;
        margin-left: 100px;
    }
    .is-receiver {
        text-align: left;
        margin-right: 100px;
    }
    .chat-box {
        flex: 1;
        display: flex;
        flex-direction: column;
        overflow-y: auto;
    }
</style>

<Collection path={'/chat'} let:ref={chatsRef} let:data={messages} on:data={scrollToTheEnd}>
    <div class="box chat-box" bind:this={chatsElement}>
        {#each messages.sort((a, b) => a.date - b.date) as message}
            <div class="notification {message.uid === user.uid ? 'is-info is-sender' : 'is-success is-receiver'}">
                {message.message}
            </div>
        {/each}
    </div>
    <AppendMessage {chatsRef} {user} />

</Collection>

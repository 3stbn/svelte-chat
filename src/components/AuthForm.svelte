<script>
    export let auth
    let email = ''
    let password = ''
    let mode = 'signIn'

    async function handleSubmit() {
        if (mode === 'signIn') {
            await auth.signInWithEmailAndPassword(email, password)
        } else {
            await auth.createUserWithEmailAndPassword(email, password)
        }

        email = ''
        password = ''
    }
</script>

<style>
    .link {
        cursor: pointer;
    }
</style>

<h1 class="title has-text-info has-text-centered">Svelte Chat</h1>
<h2 class="title">{mode === 'signIn' ? 'Sign In' : 'Sign Up'}</h2>
<form on:submit|preventDefault={handleSubmit}>
    <div class="field">
        <label class="label">Email</label>
        <input type="email" class="input" bind:value={email} required />
    </div>
    <div class="field">
        <label class="label">Password</label>
        <input type="password" class="input" bind:value={password} required />
    </div>
    <div class="field">
        <input type="submit" class="button is-fullwidth" value="Enter Chat" />
    </div>

</form>
<hr />
{#if mode === 'signIn'}
    <p>
        Do you not have an account ?
        <span class="has-text-link link" on:click={() => (mode = 'signUp')}>Sign Up</span>
    </p>
{:else}
    <p>
        Do you already have an account ?
        <span class="has-text-link link" on:click={() => (mode = 'signIn')}>Sign In</span>
    </p>
{/if}

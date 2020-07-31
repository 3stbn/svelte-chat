<script>
    import { FirebaseApp, User } from 'sveltefire'
    import firebase from 'firebase/app'
    import 'firebase/firestore'
    import 'firebase/auth'
    import Chats from './components/Chats.svelte'
    import AuthForm from './components/AuthForm.svelte'

    let firebaseConfig = {
       // your firebase configuration here
    }
    firebase.initializeApp(firebaseConfig)
</script>

<style>
    .app {
        min-height: 100vh;
        display: flex;
        flex-direction: column;
        max-height: 100vh;
    }
</style>

<main class="container section app">

    <FirebaseApp {firebase}>
        <User let:user let:auth>
            <Chats {user} />
            <button class="button is-fullwidth" on:click={() => auth.signOut()}>Leave Chat</button>
            <div slot="signed-out">
                <AuthForm {auth} />
            </div>
        </User>

    </FirebaseApp>

</main>

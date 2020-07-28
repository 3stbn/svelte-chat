<script>
    import { FirebaseApp, User } from 'sveltefire'
    import firebase from 'firebase/app'
    import 'firebase/firestore'
    import 'firebase/auth'
    import Chats from './components/Chats.svelte'
    import AuthForm from './components/AuthForm.svelte'

    let firebaseConfig = {
        apiKey: 'AIzaSyABGSgGJKiXDFac6owmWsYI1iucofbTuxI',
        authDomain: 'tutorials-7dfbb.firebaseapp.com',
        databaseURL: 'https://tutorials-7dfbb.firebaseio.com',
        projectId: 'tutorials-7dfbb',
        storageBucket: 'tutorials-7dfbb.appspot.com',
        messagingSenderId: '739505788883',
        appId: '1:739505788883:web:bfcb6e72e7c1d87f36c126',
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

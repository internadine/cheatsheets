# Authentication

### Signing up new Users

    // create useSignup.js in composables folder

    import {ref} from "vue"

    // firebase imports
    import {auth} from "../../initfirestore.js"
    import { createUserWithEmailAndPassword} from "firebase/auth"

    const error = ref(null)
    const isPending = ref(false)

    const signup = async (email, password) => {
        error.value = null
        isPending = true

        try {
            const res = await createUserWithEmailAndPassword(auth, email, password)
            if (!res) {
                throw new Error('Could not complete signup')
            }

            error.value = null
            isPending.value = false
        }
        catch (err) {
            console.log(err.message)
            error.value = err.message
            isPending.value = false
        }
    }

    const useSignup = () => {
        return { error, isPending, signup}
    }

    export default useSignup

    // use useSignup from insight the Signup.vue component in setup function

    <script>

    import {ref} from 'vue'
    import {useRouter} from 'vue-router'
    import useSignup from '../composables/useSignup'

    export default {
        setup () {
            const email = ref('')
            const password = ref('')

            const {signup, error} = useSignup()
            const router = useRouter()

            const handleSubmit = async() => {

                await signup(email.value, password.value)

                if(!error.value) {
                    router.push('/')
                }

            return {email, password, handleSubmit}
            }



    }

    </script>

### Logout User

    <script>
    import {auth} from "../../initfirestore.js"
    import {signOut} from 'firebase/auth'

    export default{
        setup() {
            const handleClick = () => {
                signOut(auth)
            }
            return { handleClick}
        }
    }

    </script>

### Logging Users In

    // create composable useLogin.js

    import {ref} from "vue"

    // firebase imports
    import {auth} from "../../initfirestore.js"
    import { signInWithEmailAndPassword} from "firebase/auth"

    const error = ref(null)
    const isPending = ref(false)

    const login = async (email, password) => {
        error.value = null
        isPending = true

        try {
            const res = await signInWithEmailAndPassword(auth, email, password)
            if (!res) {
                throw new Error('Could not complete login')
            }

            error.value = null
            isPending.value = false
        }
        catch (err) {
            console.log(err.message)
            error.value = err.message
            isPending.value = false
        }
    }

    const useLogin = () => {
        return { error, isPending, login}
    }

    export default useLogin

    // use in Login Component same concept as for Signup

### Getting Current User

    // create composable getUser.js in composables folder

    import {ref} from 'vue'

    // firebase imports
    import {auth} from "../../initfirestore.js"
    import {onAuthStateChanged} from 'firebase/auth'

    // refs
    const user = ref(auth.currentUser)

    // auth changes

    onAuthStateChanged(auth, (_user) => {
        console.log("User State changed. Current user is ", _user)
        user.value = _user
    })

    const getUser = () => {
        return {user}
    }

    export default getUser

    // user e.g. in Navbar component

### Waiting for Auth to be Ready

    // add to main.js

    import { createApp } from 'vue'
    import App from './App.vue'
    import router from './router'

    // firebaes imports
    import {auth} from "../../initfirestore.js"
    import {onAuthStateChanged} from 'firebase/auth'

    let app

    onAuthStateChanged(auth, () => {
        // only mount application once, when we first open the app, firebase is figuring out authentication status, before app mounts
        if(!app) {
            app = createApp(App).use(router).mount('#app')
        }
    })

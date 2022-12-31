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

### Route Guard

    // add to router index.js

    import Home from '../views/Home.vue'
    import Login from '../views/Login.vue'

    // firebase imports
    import {auth} from "../../initfirestore.js"

    const requireAuth = (to, from, next) => {
        let user = auth.currentUser
        if (!user) {
            // redirect to login page
            next({name: 'Login'})
        } else {
            next()
        }
    }

    const routes = [
        {
            path: '/',
            name: 'Home',
            component: Home,
            beforeEnter: requireAuth
        },
        {
            path: '/login',
            name: 'Login',
            component: Login,
            beforeEnter: requireAuth
        },...

    ]

### Redirecting Users, after logging out

    // add code to navbar, where we already use composable getUser()

    <script>
    import {getUser} from '../composables/getUser'
    import {useRotuer} from 'vue-router'
    import {watchEffect} from 'vue'

    // firebase imports
    import {auth} from "../../initfirestore.js"
    import {signOut} from 'firebase/auth'

    export default {
        setup() {
            const {user} = getUser()
            const router = useRouter()

            const handleClick = () => {
                singOut(auth)
            }

            watchEffect(() => {
                if(!user.value) {
                    router.push('/login')
                }
            })

            return {handleclick, user}


        }
    }
    </script>

### Getting firestore content based on user id (e.g. only see your content)

    // user Id has been saved to User Object in Firstore
    // add to getCollection.js in composables

    import {ref, watchEffect} from 'vue'

    // firebase imports
    import {db} from '../../initfirstore.js'
    import {collection, onSnapshot, query, where} from 'firebase/firestore'

    const getCollection = (c, q) =>  {
        const documents = ref(null)

        // collection reference
        let colRef = collection(db, c)

        if(q) {
            colRef = query(colRef, where(...q))
        }


        const unsub = onSnapshot(colRef, snapshot ={
            let results = []
            snapshot.docs.forEach( doc => {
                results.push({...doc.data(), id: doc.id})
            })

            // udate values
            documents.value = results
        })
    }

    // pass q in from Home.vue when the initial query to firstore starts

    ...
    setup() {
        const {user} = getUser()
        const {documents: books} = getCollection(
            'books',
            ['userUid', '==', user.value.uid ]
        )
    }

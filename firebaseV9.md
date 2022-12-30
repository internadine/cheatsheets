## Firebase V9

### Include to project

    import { initializeApp } from "firebase/app";
    import { getFirestore } from "firebase/firestore";
    import {getAuth} from 'firebase/auth'

    const firebaseConfig = {
    // ...
    };

    initializeApp(firebaseConfig);

    const db = getFirestore()
    const auth = getAuth()

    export {db, auth}

### Fetch Data from Firestore (Componsition API)

    import {ref} from 'vue'
    import db from '../../initfirestore'
    import {collection, getDocs} from 'firebase/firestore'

    export default {

        setup() {
            const books = ref([])

            const colRef = collection(db, 'books')

            getDocs(colRef)
                .then(snapshot => {
                    let docs = []
                    snapshot.docs.forEach(doc => {
                        docs.push({...doc.data(), id: doc.id})
                    })
                    books.value = docs
                })


            return {books}
        }
    }

### Submit Data to Firestore (Composition API)

    import {ref} from 'vue'
    import db from '../../initfirestore.js'
    import {addDocs, collection} from 'firebase/firestore'

    export default {

        setup() {
            const author = ref('')
            const title = ref('')

            const handleSubmit = async () => {
                const colRef = collection(db, 'books')

                await addDocs(colRef, {
                    title: title.value,
                    author: author.value,
                    isFav: true
                    })
                // reset the form
                author.value = ''
                title.value = ''
            }
            return {author, title, handleSubmit}
        }
    }

### Delete Document

    import db from ../../initfirestore.js
    import { doc, deleteDoc } from 'firebase/firestore'

    export default {
        name: 'Home',
        setup() {
            const handleDelete = (book) => {
                const docRef = doc(db, 'books', book.id)

                deleteDoc(docRef)
            }
            return {handleDelete}
        }
    }

### Update Document

    import db from ../../initfirestore.js
    import { doc, updateDoc } from 'firebase/firestore'

    export default {
        name: 'Home',
        setup() {
            const handleUpdate = (book) => {
                const docRef = doc(db, 'books', book.id)

                updateDoc(docRef, {
                    title: 'new value'
                })
            }
            return {handleUpdate}
        }
    }

# Vue3 Composition API

## Example with setup function incl. computed properties, watch and watchEffect

    <template>
        <div class="center">

            <input
            type="text"
            v-model="search"
            >
        <div
            v-for="name in matchingNames"
            :key="name"
        >{{name}}</div>
        <button
        class="button"
        @click="changeName"
        >Change my name</button>
        </div>
     </template>

    <script>

    // import only features, that you need

     import { computed, onMounted, ref, watch } from "vue";

    export default {

        // setup function fires first of all lifecycle hooks

        setup() {
            // ref is an object with a value property - that is why you need to access value with eg. search.value
            const search = ref("");
            const names = ref(["John", "Jane", "Joe", "Jack", "Jill", "Jenny"]);

            // you can watch a ref like this, eg. search ref

            watch(search, () => {
                console.log('watch function run')
            })

            // similar, you can use watchEffect, but watchEffect also runs, when setup function first runs - here it will watch search.value
            // so you can use it to collect data from database

            watchEffect(() => {
                console.log('watchEffect function ran', search.value)
            })

            //computed property in setup function

            const matchingNames = computed(() => {
                return names.value.filter((name) => name.includes(search.value));
            });

            onMounted(() => {
                console.log("mounted");
            });

        // return everything, that you want to use in template

        return { names, search, matchingNames };
        },
    };
    </script>

## Using Props

    // Home View

    <template>
        <div class="home">
            <h1>Home</h1>
            <PostList :posts="posts"/>
        </div>
    </template>

    <script>
    import {ref} from 'vue'
    import PostList from '../components/Postlist.vue'

    name: "Home",
    components: {
        PostList
    }

    setup() {

        const posts = ref([
            {title: "welcome", body: "lorem ipsume", id: 1},
            {title: "top tips", body: "lorem ipsume 2", id: 2}
        ])

        return {posts}
    }

    </script>

    // PostList.vue component

    <template>
        <div class="post-list">
            <div v-for="post in posts" :key="post.id">
                <h3>{{post.title}}</h3>
            </div>
        </div>
    </template>

    <script>
    export default {
        props: ['posts']
        // access posts in setup function through props
        setup(props){
            console.log(props.posts)
        }
    }
    </script>

## Lifecycle Hooks

    <template>
        <div>
            <h1>Home</h1>
        </div>

    </template>

    <script>
    import {onMounted, onUnmounted, onUpdated} from 'vue'

    export default {
        setup() {
            onMounted(() => console.log('component mounted'))
            onUnmounted(() => console.log('component unmounted'))
            onUpdated(() => console.log('component updated, because component has been rerendered'))

        }
    }

    </script>

## Async Code

    <script>
    import { ref } from 'vue'

    export default {
        name: 'Home',
        setup() {
            const posts = ref([])
            const error = ref(null)

            const load = async () => {
                try {
                    const data = await fetch('http:localhost:3000/posts')
                    if(!data.ok) {
                        throw Error('no data available')
                    }
                    posts.value = await data.json()
                } catch(err) {
                    error.value = err.message
                }
            }
            load()
            return {error, posts}
        }

    }



    </script>

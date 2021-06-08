<template>
    <div class="dashboard">
        <h3>Hello, <span v-if="users">{{ users[0].name }}</span> <br/> Welcome</h3>
    </div>
    <ul v-if="users">
        <li>
            <b>NAME:</b> {{ users[0].name }}
        </li>
        <br>
        <li>
            <b>COUNTRY:</b> {{ users[0].country }}
        </li>
    </ul>
    <div v-else>loading...</div>
    <Button content="Add User" bgcolor="green" color="#fff" @click="addUserForm"/>
    <Button :content="listButtonContent" bgcolor="skyBlue" color="#000" @click="showFriendsList"/>
    <ul v-if="show && users">
        <div v-for="user in users" :key="user.id">
            <router-link :to="{name: 'FriendsData', params: {id: user.id}}">
                <li>
                    Name: {{ user['name'] }}
                    <br>
                    Country: {{ user['country'] }}
                </li>
            </router-link>
        </div>
    </ul>
    <Alert v-if="showForm">
        <form @submit="addUser">
            <input type="text" v-model="user" name="user" placeholder="Surname"/>
            <br>
            <input type="text" v-model="country" name="country" placeholder="Country"/>
            <br>
            <Button bgcolor="#42b983" type="submit" content="Submit"/>
            <Button bgcolor="red" color="white" @click="addUserForm">
                <b>X</b> Close
            </Button>
        </form>
    </Alert>
</template>

<script>

import Button from '@/components/Button.vue'
import Alert from '@/components/Alert.vue'

export default {
    name: 'Dashboard',
    components: {
        Button, 
        Alert
    },
    props: ['model'],
    data () {
        return {
            user: '',
            country: '',
            show: false,
            showForm: false,
            listButtonContent: 'Friends List',
            users: null,
        }
    },
    methods : {
        addUserForm () {
            this.showForm = !this.showForm
        },
        showFriendsList () {
            this.show = !this.show,
            this.listButtonContent = (this.show == true) ? 'X Close List' : 'Friends List'
        },
        async addUser(e, user) {
            e.preventDefault()

            let newUser = {
                name: this.user,
                country: this.country
            }
            const requestOptions = {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify(newUser)
            }
            const url = 'http://localhost:3000/users'
            const res = await fetch(url, requestOptions)
            const data = await res.json()
            this.users = [...this.users, data],

            this.user = '',
            this.country = '',
            this.showForm = !this.showForm
        }
    },
    async created() {
        const LoadData = async () => {
            try {
                const url = 'http://localhost:3000/users'
                const res = await fetch(url)
                const data = await res.json()
                return data
            } 
            catch (err) {
                console.log(err)
            }
        }
        LoadData().then((data) => {
            this.users = data
        })
    }
}

</script>

<style scoped>
ul {
    margin: 10px 50px;
    padding: 10px;
    border: 2px solid #2c3e50;
    border-radius: 10px;
    display: block;
    overflow: none;
    background: #42b983;
    color: #fff;
}
ul li {
    margin: 5px;
    padding: 5px;
    border-radius: 5px;
    background: #2c3e50;
}
ul a {
    text-decoration: none;
    color: #fff;
}
ul a:hover {
    background: #2a5c5f;
}
ul a.router-link-exact-active {
    background: #2a5c5f;
}
input {
    margin: 10px;
    padding: 5px;
    border-radius: 10px;
    border: midnightblue;
    box-sizing: border-box;
    background: #fff;
    width: 100%;
}
</style>
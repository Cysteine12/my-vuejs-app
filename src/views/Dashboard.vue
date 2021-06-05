<template>
    <div class="dashboard">
        <h3>Hello, {{ users[0].name }} <br/> Welcome</h3>
    </div>
    <ul>
        <li>
            <b>NAME:</b> {{ users[0].name }}
        </li>
        <br>
        <li>
            <b>COUNTRY:</b> {{ users[0].country }}
        </li>
    </ul>
    <Button content="Change Data" bgcolor="green" color="#fff" @click="changeDataF"/>
    <Button :content="listButtonContent" bgcolor="skyBlue" color="#000" @click="showFriendsList"/>
    <ul v-if="show">
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
    <Alert v-if="changeData">
        <form @submit="onSubmit">
            <input type="text" v-model="user" name="user" placeholder="Surname"/>
            <br>
            <input type="text" v-model="country" name="country" placeholder="Country"/>
            <br>
            <Button type="submit" content="Submit"/>
            <Button bgcolor="red" color="white" @click="changeDataF">
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
            changeData: false,
            listButtonContent: 'show friends list',
            users: [],
        }
    },
    methods : {
        changeDataF () {
            this.changeData = !this.changeData
        },
        showFriendsList () {
            this.show = !this.show,
            this.listButtonContent = (this.show == true) ? 'Close List' : 'Show Friends List'
        },
        onSubmit (e) {
            e.preventDefault()

            const newUser = {
                user: this.users[0].name,
                country: this.users[0].country
            }
            console.log(newUser)
        }
    },
    mounted() {
        fetch('http://localhost:3000/users')
            .then(res => res.json())
            .then(data => this.users = data)
            .catch(err => console.log(err.message)),
            console.log(data)
    }
}

</script>

<style scoped>
button {
    border: 1.5px solid #2c3e50;
    border-radius: 5px;
    padding: 3px;
    background: #42b983;
}
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

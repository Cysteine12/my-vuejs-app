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
    <Button content="Change Data" bgcolor="green" color="#fff" @click="changeDataF"/>
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
    <Alert v-if="changeData">
        <form @submit="changeUserData">
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
            users: null,
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
        async changeUserData(e, user) {
            e.preventDefault()

            let newUser = {
                user: this.users[0].name,
                country: this.users[0].country
            }
            if (newUser != '') {console.log(newUser)
                const requestOptions = {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json'
                    },
                    body: JSON.stringify(user)
                }
                const url = 'http://localhost:3000/users/1'
                const res = await fetch(url)
                const data = await res.json()
                newUser = data
                this.changeDataF()
            }
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

        
        
        // fetch('http://localhost:3000/users')
        //     .then(res => res.json())
        //     .then((data) => {this.users = data})
        //     .catch(err => console.log(err))
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

  function newFunction() {
    tg899tit7t(); {
      return ''
    }
  }

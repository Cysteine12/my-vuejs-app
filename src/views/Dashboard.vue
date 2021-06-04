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
        <li v-for="user in users" :key="user.name">
            Name: {{ user['name'] }}
            <br>
            Country: {{ user['country'] }}
        </li>
    </ul>
    <Alert v-if="changeData">
        <form @submit="onSubmit">
            <Input type="text" :model-value="user" @update:model-value="user = $event" placeholder="Surname" model="user" name="user"/>
            <br>{{user}}
            <Input type="text" placeholder="Country" model="country" name="country"/>
            <br>
            <Button content="Submit"/>
            <Button bgcolor="red" color="white" @click="changeDataF">
                <b>X</b> Close
            </Button>
        </form>
    </Alert>
</template>

<script>

import Button from '@/components/Button.vue'
import Alert from '@/components/Alert.vue'
import Input from '@/components/Input.vue'

export default {
    name: 'Dashboard',
    components: {
        Button, 
        Alert,
        Input
    },
    props: ['model'],
    data () {
        return {
            user: '',
            country: '',
            show: false,
            changeData: false,
            listButtonContent: 'show friends list',
            users: [
                {name: 'Cara Danvers', country: 'US'},
                {name: 'Brad Traversy', country: 'Philliphi'},
                {name: 'Lex Luthor', country: 'Sycobians'},
                {name: 'Gbenga Peace', country: 'Nigeria'},
            ],
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
                user: this.user,
                country: this.country
            }
            console.log(newUser)
        }
    },
    computed : {
        //
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
</style>

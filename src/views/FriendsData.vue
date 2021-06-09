<template>
    <h2 v-if="user">About {{ user.name }}</h2>
    <ul v-if="user">
        <li>Name: {{ user.name }}</li>
        <li>Country: {{ user.country }}</li>
        <li>Route ID: {{ id }}</li>
    </ul>
    <div v-else>loading....</div>
    <Button content="back" bgcolor="blue" color="white" @click="back"/>
    <Button content="Edit" bgcolor="yellow" color="white" @click="editUser"/>
    <Button content="Delete" bgcolor="red" color="white" @click="deleteUser"/>
    <Alert v-if="showEditForm">
        <form @submit="submitEditForm">
            <input type="text" v-model="name" name="name">
            <input type="text" v-model="country" name="country">
            <Button bgcolor="#42b983" type="submit" content="Submit"/>
            <Button bgcolor="red" color="#fff" @click="!this.showEditForm">
                <b>X</b> Close
            </Button>
        </form>
        <br/>
    </Alert>
</template>

<script>

import Button from '@/components/Button.vue'
import Alert from '@/components/Alert.vue'

export default {
name: 'FriendsData',
components: {
    Button,
    Alert
},
props: ['id'],

data () {
    return {
        user: null,
        name: '',
        country: '',
        showEditForm: false
    }
},
methods: {
    back() {
        this.$router.go(-1)
    },
    editUser() {
        this.name = this.user.name,
        this.country = this.user.country,
        this.showEditForm = true
    },
    submitEditForm(e) {
        e.preventDefault()
        const EditData = async () => {
            try {
                let formData = {
                    name : this.name,
                    country: this.country
                }
                const url = `http://localhost:3000/users/${this.id}`

                const requestOptions = {
                    method: 'PUT',
                    headers: {
                        'Content-Type' : 'application/json'
                    },
                    body: JSON.stringify(formData)
                }
                const res = await fetch(url, requestOptions)
                const data = await res.json()
                return data
            }
            catch(err) {
                console.log(err)
            }
        }
        EditData().then((data) => {
            this.user = data

            this.name = ''
            this.country = ''
            this.showEditForm = false
        })
    },
    deleteUser() {
        const DeleteUser = async () => {
            try {
                const url = `http://localhost:3000/users/${this.id}`

                const requestOptions = {
                    method: 'DELETE'
                }
                const res = await fetch(url, requestOptions)
                return res
            }
            catch {
                alert('Error deleting user')
            }
        }
        if (confirm('Are you sure?')) {
            DeleteUser().then((res) => {
                if (res.ok) {
                    this.$router.go(-1)
                    alert(`${this.user.name} has been deleted successfully`)
                } else {
                    alert('Error deleting user')
                }
            })
        }
    }
},
mounted() {
    fetch(`http://localhost:3000/users/${this.id}`)
        .then(res => res.json())
        .then(data => this.user = data)
        .catch(err => console.log(err.message))
    }
}
</script>

<style>
#app {
    text-align: center;
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
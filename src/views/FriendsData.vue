<template>
    <h2 v-if="user">About {{ user.name }}</h2>
    <ul v-if="user">
        <li>Name: {{ user.name }}</li>
        <li>Country: {{ user.country }}</li>
        <li>Route ID: {{ id }}</li>
    </ul>
    <div v-else>loading....</div>
    <Button content="back" bgcolor="blue" color="white" />
</template>

<script>

import Button from '@/components/Button.vue'

export default {
name: 'FriendsData',
components: {
    Button
},
props: ['id'],
data () {
    return {
        user: null
    }
},
mounted() {
    fetch('http://localhost:3000/users/' + this.id)
        .then(res => res.json())
        .then(data => this.user = data)
        .catch(err => console.log(err.message))
}
// computed: {
//     filteredUser : this.users.filter((user) => {
//         return user.id == this.id
//     }),
// }
}
</script>

<style>
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
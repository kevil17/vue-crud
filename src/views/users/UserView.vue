<script>
import axios from "axios";
import { RouterLink } from "vue-router";
export default {
    name: "UserView",
    data() {
        return {
            users: []
        };
    },
    methods: {
        getUsers() {
            axios.get("http://localhost:8080/v1/users?detailed=true").then(res => {
                this.users = res.data;
                console.log(this.users);
            }).catch(function (error) {
                //handleErrors
            });
        },
        deleteUserById(userId){
            if(confirm('Are you sure, you want to delete this data?'));
            axios.delete(`http://localhost:8080/v1/users/${userId}`).then(res => {
                this.getUsers();
            }).catch(function (error) {
                //handleErrors
            });
        },
    },
    mounted() { this.getUsers(); },
    components: { RouterLink }
}
</script>
<template>
    <h1>List Users</h1>
    <div class="course">
        <div class="card">
            <div class="card-header">
                <h4>
                    Users
                    <RouterLink to="/users/create" class="btn btn-primary float-end">
                        Add User
                    </RouterLink>        
                </h4>
            </div>
            <div class="card-body">
                <table class="table table-bordered">
                    <thead>
                        <tr>
                            <th>Nro.</th>
                            <th>firstName</th>
                            <th>lastName</th>
                            <th>birthDay</th>
                            <th>age</th>
                            <th>email</th>
                            <th>userName</th>
                            <th>password</th>
                        </tr>
                    </thead>
                    <tbody v-if="this.users.length > 0">
                        <tr v-for="(user, index) in this.users">
                            <td>{{index+1}}</td>
                            <td>{{user.userDetailDTO.firstName}}</td>
                            <td>{{user.userDetailDTO.lastName}}</td>
                            <td>{{user.userDetailDTO.birthDay}}</td>
                            <td>{{user.userDetailDTO.age}}</td>
                            <td>{{user.email}}</td>
                            <td>{{user.userName}}</td>
                            <td>{{user.password}}</td>
                            <td>
                                <RouterLink :to="{path: '/users/'+ user.id +'/edit'}" class="btn btn-success">
                                     Edit User
                                </RouterLink>  
                                <button type="button" @click="deleteUserById(user.id)" class="btn btn-danger">
                                Delete</button>
                            </td>
                        </tr>
                    </tbody>
                    <tbody v-else>
                        <tr>
                            <td colspan="8">there are not users</td>
                        </tr>
                    </tbody>
                </table>
            </div>
        </div>
    </div>
</template>
<style scoped>
</style>
<script>
import axios from "axios";
import { RouterLink } from 'vue-router';
export default {
    name: "UserEdit",
    data() {
        return {
            userId:'',
            model: {
                user: {
                    userName: '',
                    password: '',
                    email: '',
                    userDetailDTO: {
                        firstName: '',
                        lastName: '',
                        birthDay: '',
                        age: '',
                    }
                }
            },errors: [],
        };
    },
    methods: {
        getUserById(userId){
            axios.get(`http://localhost:8080/v1/users/${userId}`).then(res => {
                this.model.user = res.data;
                console.log(this.users);
            }).catch(function (error) {
                //handleErrors
            });
        },
        editUser() {
            this.errors = [];
            if(this.model.user.userDetailDTO.firstName === ''){
                this.errors.push('The first name is required');
            }else if(this.model.user.userDetailDTO.lastName === ''){
                this.errors.push('Last name is required');
            }else if(this.model.user.userDetailDTO.birthDay === ''){
                this.errors.push('Birthday is required');
            }else if(this.model.user.userDetailDTO.age === ''){
                this.errors.push('Age is required');
            }else if (this.model.user.userName === '') {
             this.errors.push('User name is required.');
            }else if(this.model.user.password === ''){
                this.errors.push('Password is mandatory.');
            }else if(this.model.user.email === ''){
                this.errors.push('Email is required');
            }else{
                axios.put(`http://localhost:8080/v1/users/${this.userId}`, this.model.user)
                .then(res => {
                alert('User was edited Successful');
                
            }).catch(function (error) {
                //handle error on UI
            });
            }
            
        }
    }, mounted(){
        this.userId = this.$route.params.id;
        this.getUserById(this.userId);
    },
    components: { RouterLink }
}
</script>
<template>
    <h1>Form Edit User</h1>
    <div class="container mt-5">
        <div class="card">
            <div class="card-header">
                <h4>Edit Users</h4>
                <p v-if="errors.length">
                    <b>Por favor, corrija el(los) siguiente(s) error(es):</b>
                 <ul>
                    <li v-for="error in errors">{{ error }}</li>
                </ul>
                </p>
            </div>
            <div class="card-body">
                <div class="mb-3">
                    <label for="">firstName</label>
                    <input type="text" v-model="this.model.user.userDetailDTO.firstName" class="form-control">
                </div>
                <div class="mb-3">
                    <label for="">lastName</label>
                    <input type="text" v-model="this.model.user.userDetailDTO.lastName" class="form-control">
                </div>
                <div class="mb-3">
                    <label for="">birthDay</label>
                    <input type="text" v-model="this.model.user.userDetailDTO.birthDay" class="form-control">
                </div>
                <div class="mb-3">
                    <label for="">age</label>
                    <input type="text" v-model="this.model.user.userDetailDTO.age" class="form-control">
                </div>
                <div class="mb-3">
                    <label for="">userName</label>
                    <input type="text" v-model="this.model.user.userName" class="form-control">
                </div>
                <div class="mb-3">
                    <label for="">password</label>
                    <input type="text" v-model="this.model.user.password" class="form-control">
                </div>
                <div class="mb-3">
                    <label for="">email</label>
                    <input type="text" v-model="this.model.user.email" class="form-control">
                </div>
                <div class="mb-3">
                    <button type="button" @click="editUser" class="btn btn-primary">Edit</button> &nbsp;
                    <RouterLink to="/users" class="btn btn-primary">Back</RouterLink>
                </div>
            </div>
        </div>
    </div>
</template>
<style scoped>
</style>
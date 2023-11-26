<script>
import axios from "axios";
import { RouterLink } from 'vue-router';

export default {
    name: "UserCreated",
    data() {
        return {
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
            },
            errors: [],
        };
    },
    methods: {
        saveUser() {
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
                axios.post('http://localhost:8080/v1/users', this.model.user)
                .then(res => {
                alert('User was saved Successful');
                this.model.data = {
                    userName: '',
                    password: '',
                    email: '',
                    userDetailDTO: {
                        firstName: '',
                        lastName: '',
                        birthDay: '',
                        age: '',
                    }
                };
            }).catch(function (error) {
                //handle error on UI
            });
            }
            
        }
    },
    components: { RouterLink }
}
</script>
<template>
    <h1>Form create User</h1>
    <div class="container mt-5">
        <div class="card">
            <div class="card-header">
                <h4>Add Users</h4>
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
                    <button type="button" @click="saveUser" class="btn btn-primary">Save</button> &nbsp;
                    <RouterLink to="/users" class="btn btn-primary">Back</RouterLink>
                </div>
            </div>
        </div>
    </div>
</template>
<style scoped>
</style>
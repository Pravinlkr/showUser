<template>
<div class="header">
    <h2>User Details</h2>
    <button class="add" v-on:click="showModel()">Add New User</button>
</div>
<div class="tableBox">
    <table>
        <tr>
            <th>Full Name</th>
            <th>Email</th>
            <th>Date Of Birth</th>
            <th>Password</th>
            <th>Edit</th>
            <th>Delete</th>
        </tr>
        <tr v-for="(user,index) in userList" v-bind:key="index">
            <td>{{user.name}}</td>
            <td>{{user.email}}</td>
            <td>{{user.dob}}</td>
            <td>{{user.password}}</td>
            <td>
                <button class="edit">Edit</button>
            </td>
            <td>
                <button class="delete">Delete</button>
            </td>
        </tr>
    </table>
</div>
<div class="footer">
    <input type="checkbox" class="sortCheckbox" id="sortCheckbox">
    <label for="sortCheckbox">Sort By Date Of Birth</label>
</div>
<form-model :showModel="showModelValue" @updateModel="updateModel"></form-model>
</template>

<script>
import formModel from './formModel.vue'
export default {
    name: 'user',
    components: {
        formModel
    },
    data(){
        return{
            showModelValue:false,
            userList:[
                {name:'Manish Singh', email:'manishsingh@gmail.com', dob:'21-01-1995', password:'mainsh123'},
                {name:'Vikkey Kumar', email:'kumarVikkey@gmail.com', dob:'02-03-1993', password:'vikkey123'},
                {name:'Pradeep Yadav', email:'pradeep@gmail.com', dob:'21-01-1997', password:'pradeep007'},
                {name:'Abhishek Ranjan', email:'arj@gmail.com', dob:'21-01-1998', password:'arj@1234'},
                {name:'Ankit Kumar', email:'akumar001@gmail.com', dob:'21-01-1996', password:'akumar001'},
                ]
        }
    },
    methods:{
        showModel(){
            console.log("called");
            this.showModelValue = true;
            console.log(this.showModelValue);
        },
        updateModel(){
            console.log(this.showModelValue);
            this.showModelValue = false;
        }
    }
}
</script>

<style scoped>
.header{
    width:80%;
    height: 70px;
    margin:0 auto;
}
.header h2{
    margin:1% 2%;
    float: left;
}
button.add {
    height: 30px;
    margin:1% 2%;
    background-color: green;
    border: none;
    border-radius: 5px;
    color: white;
    padding:5px 10 px;
    float:right;
}
.tableBox{
    width: 80%;
    height: auto;
    margin:0 auto;
    text-align: center;
}
table{
    width: 100%;
}
table th{
    background-color: #303030;
    color:white;
    padding:10px 10px;
}
table td{
    padding-top: 10px;
    font-size: 16px;
}
button.edit{
    border:none;
    outline: none;
    color:white;
    background-color: #42a3ed;
    height: 30px;
    width: 70%;
}
button.delete{
    border:none;
    outline: none;
    color:white;
    background-color: #ff0d39;
    height: 30px;
    width: 70%;
}
.footer{
    height: 50px;
    background-color: #ccc;
    width: 100%;
    position:fixed;
    bottom: 0;
    text-align: center;
}
.sortCheckbox{
    height: 14px;
    width: 14px;
    margin-top: 18px;
}
.footer label{
    font-size: 15px;
}
</style>

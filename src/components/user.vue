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
        <tr v-for="(user,index) in filteredList" v-bind:key="index">
            <td>{{user.name}}</td>
            <td>{{user.email}}</td>
            <td>{{user.dob}}</td>
            <td>{{user.password}}</td>
            <td>
                <button class="edit">Edit</button>
            </td>
            <td>
                <button class="delete" v-on:click="deleteUser(user.id)">Delete</button>
            </td>
        </tr>
    </table>
</div>
<div class="footer">
    <input type="checkbox" class="sortCheckbox" id="sortCheckbox" v-on:click="sortList()" v-model="sortlistByDate">
    <label for="sortCheckbox">Sort By Date Of Birth</label>
</div>
<form-model :showModel="showModelValue" @updateModel="updateModel" @addNewUser="addNewUser"></form-model>
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
                {id:2, name:'Manish Singh', email:'manishsingh@gmail.com', dob:'1995-02-25', password:'mainsh123'},
                {id:4, name:'Vikkey Kumar', email:'kumarVikkey@gmail.com', dob:'1993-04-07', password:'vikkey123'},
                {id:6, name:'Pradeep Yadav', email:'pradeep@gmail.com', dob:'1997-01-18', password:'pradeep007'},
                {id:8, name:'Abhishek Ranjan', email:'arj@gmail.com', dob:'1998-01-26', password:'arj@1234'},
                {id:10, name:'Ankit Kumar', email:'akumar001@gmail.com', dob:'1996-10-15', password:'akumar001'},
                ],
            filter:'nonsorted',
            filteredList:[],
            sortlistByDate: false
        }
    },
    methods:{
        updateList(){
            if(this.filter == 'nonsorted'){
                this.userList.forEach(element => {
                    this.filteredList.push(element);
                });
            }
            if(this.filter == 'sorted'){
                this.userList.forEach(element => {
                    this.filteredList.push(element);
                });
                let lenoforiginalarray = this.filteredList.length;
                let i = 0;
                let j = 0;
                for(i=0; i<lenoforiginalarray; i++){
                    let dob1 = this.filteredList[i].dob;

                    for(j=i+1; j<lenoforiginalarray; j++){
                        let dob2 = this.filteredList[j].dob;

                        if(new Date(dob1) > new Date(dob2)){
                            let temp = this.filteredList[i];
                            this.filteredList[i] = this.filteredList[j];
                            this.filteredList[j] = temp;
                        }
                    }
                }
            }

        },
        showModel(){
            this.showModelValue = true;
        },
        updateModel(){
            this.showModelValue = false;
        },
        addNewUser(value){
            let len = this.userList.length;
            let lastData = this.userList[len-1];
            let newid = lastData.id+2;
            this.userList.push({id:newid, name:value.name, email:value.email, dob:value.dob, password:value.password});

            this.filteredList = [];
            this.updateList();
        },
        deleteUser(id){
            var len = this.userList.length;
            let i = 0;
            let deleteIndex = 0;
            for(i=0; i<len; i++){
                if(this.userList[i].id == id){
                    deleteIndex = i;
                }
            }
            this.userList.splice(deleteIndex,1);
            this.filteredList = [];
            this.updateList();
        },
        sortList(){
            if(this.sortlistByDate == false){
                this.filter = 'sorted';
                this.filteredList = [];
                this.updateList();
            }
            else{
                this.filter = 'nonsorted';
                this.filteredList = [];
                this.updateList();
            }
            
        }
    },
    mounted(){
        this.updateList();
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

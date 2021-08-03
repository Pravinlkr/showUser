<template>
<div class="model" v-if="showModel">
    <div class="modal-content">
        <div class="modelHeader">
            <h3>Add New User</h3>
            <button v-on:click="closeModel()">X</button>
        </div>
        <div class="modelBody">
            <p class="errormsg">{{errorMessage}}</p>
            <label for="email">Email :</label><br />
            <input type="email" class="email" id="email" placeholder="Email" v-model="email"><br />

            <label for="name">Full Name :</label><br />
            <input type="text" class="name" id="name" placeholder="Full Name" v-model="name"><br />

            <label for="dob">Date Of Birth :</label><br />
            <input type="date" class="dob" id="dob" placeholder="Date Of Birth" v-model="dob"><br />

            <label for="password">Password :</label><br />
            <input type="password" class="password" id="password" placeholder="Password" v-model="password"><br />

            <label for="cpassword">Confirm Password :</label><br />
            <input type="password" class="cpassword" id="cpassword" placeholder="Confirm Password" v-model="cpassword"><br />
            <input type="checkbox" class="termCondition" id="termCondition" v-model="termCondition">
            <label for="termCondition" class="termConditionLabel">I accept all terms and conditions.</label><br />
            <button class="add" v-on:click="addData()">Add</button>
        </div>
    </div>
</div>
</template>

<script>
export default {
    name: 'formModel',
    props:{
        showModel:{
            type:Boolean,
            default:false
        }
    },
    data(){
        return{
            errorMessage:'',
            name:'',
            email:'',
            dob:'',
            password:'',
            cpassword:'',
            termCondition:true
        }
    },
    methods: {
        closeModel() {
            this.$emit('updateModel');
        },
        addData(){
            if(this.name.length>0 && this.email.length > 0 && this.dob.length>0 && this.password.length > 0 && this.cpassword.length>0 && this.termCondition == true){
                if(this.password == this.cpassword){
                    this.$emit('addNewUser', {name:this.name, email:this.email, dob:this.dob, password:this.password});
                    this.$emit('updateModel');
                    this.name = '';
                    this.email = '';
                    this.dob = '';
                    this.password = '';
                    this.cpassword = '';
                }
                else{
                    this.errorMessage = 'Password and confirm password are not same, try again'
                }
            }
            else{
                this.errorMessage = "All fields are required, please try again"
            }
        }
    }
}
</script>

<style scoped>
.model {
    position: fixed;
    /* Stay in place */
    z-index: 1;
    overflow: auto;
    /* Enable scroll if needed */
    background-color: rgb(0, 0, 0);
    /* Fallback color */
    background-color: rgba(0, 0, 0, 0.4);
    padding-top: 30px;
    /* Location of the box */
    left: 0;
    top: 0;
    width: 100%;
    /* Full width */
    height: 100%;
}

.modal-content {
    background-color: #fefefe;
    margin: auto;
    padding: 10px;
    border: 1px solid #888;
    width: 50%;
}

.modelHeader {
    height: 50px;
    margin-bottom: 1%;
    width: 100%;
    border-bottom: 1px solid #ccc;
}

.modelHeader h3 {
    margin: 2% 2%;
    float: left;
}

.modelHeader button {
    margin: 2% 2%;
    float: right;
}
.errormsg{
    text-align: center;
    font-size: 15px;
    color:orange;
}
label {
    font-size: 15px;
    font-weight: 500;
    margin: 2% 25%;
}

input {
    border: 1px solid #ccc;
    height: 30px;
    margin: 2% 25%;
    width: 50%;
    outline:none;
}

label.termConditionLabel {
    margin: 2% 1%;
}

input.termCondition {
    width: 15px;
    height: 15px;
    margin-right: 1%;
}

button.add {
    height: 30px;
    background-color: green;
    border: none;
    border-radius: 5px;
    color: white;
    width: 80px;
    margin: 2% 45%;
}
</style>

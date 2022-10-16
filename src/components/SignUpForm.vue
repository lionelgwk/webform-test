<template>
    <form @submit.prevent="submitForm">
        <label>Email:</label>
        <input type="email" required v-model="email"/>

        <label>Password:</label>
        <input type="password" required v-model="password"/>
        <div v-if="passwordError" class="error">{{passwordError}}</div>

        <label>Role:</label>
        <select v-model="role">
            <option value="developer">Web Developer</option>
            <option value="designer">Web Designer</option>
        </select>
        
        <!-- <div>
            <input type="checkbox" value="amy" v-model="names" />
            <label>Amy</label>
        </div>
        <div>
            <input type="checkbox" value="betty" v-model="names" />
            <label>Betty</label>
        </div>
        <div>
            <input type="checkbox" value="camille" v-model="names" />
            <label>Camille</label>
        </div> -->

        <div class="skills">
            <label>Skills:</label>
            <input type="text" required v-model="tempSkill" @keyup="addSkill" />
        </div>

        <div v-for="skill in skills" class="pill">
            <span @click="deleteSkill(skill)">{{skill}}</span>
        </div>

        <div class="terms">
            <input type="checkbox" required v-model="terms" />
            <label>Accept Terms and Conditions</label>
        </div>

        <div class="submit">
            <button>Create an Account</button>
        </div>

    </form>

    <p>Email: {{email}}</p>
    <p>Password: {{password}}</p>
    <p>Role: {{role}}</p>
    <p>Terms accepted: {{terms}}</p>
    <!-- <p>Names: {{names}}</p> -->
    <!-- <p>Skills:</p> -->

</template>

 
<script>
export default {
    data(){
        return{
            email: '',
            password: '',
            role: 'designer',
            terms: false,
            tempSkill: '',
            skills: [],
            passwordError: ''
            // names: []
        }
    },
    methods:{
        addSkill(event){
            if (event.key === 'Enter' && this.tempSkill.length > 0){
                if (!this.skills.includes(this.tempSkill)){
                    this.skills.push(this.tempSkill);
                }
                this.tempSkill = "";
            }
            
        },
        deleteSkill(skill){

            // Method 1
            this.skills = this.skills.filter((item) => {
                return skill !== item;
            })
            
            // Method 2
            // const index = this.skills.indexOf(skill);
            // this.skills.splice(index, 1);
        },
        submitForm(){
            this.passwordError = this.password.length > 5 ? '' : 'Password must have at least 6 characters.';
        }
    }

}
</script>


<style>

    form {
        max-width: 420px;
        margin: 30px auto;
        background: white;
        text-align: left;
        padding: 40px; border-radius: 10px;
    }
    label {
        color: #aaa;
        display: inline-block;
        margin: 25px 0 15px;
        font-size: 0.6em;
        text-transform: uppercase;
        letter-spacing: 1px;
        font-weight: bold;
    }
    input {
        display:block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555;
    }
    input, select{
        display: block;
        padding: 10px 6px;
        width: 100%;
        box-sizing: border-box;
        border: none;
        border-bottom: 1px solid #ddd;
        color: #555;
    }
    input[type="checkbox"] {
        display: inline-block;
        width: 16px;
        margin: 0 10px 0 0;
        position: relative;
        top: 2px;
    }
    .pill{
        display: inline-block;
        margin: 20px 10px 0 0;
        padding: 6px 12px;
        background: #eee;
        border-radius: 20px;
        font-size: 12px;
        letter-spacing: 1px;
        font-weight: bold;
        color: #777;
        cursor: pointer;
    }
    button {
        background: #0b6dff;
        border: 0;
        padding: 10px 20px;
        margin-top: 20px;
        color: white;
        border-radius: 20px;
    }
    .submit {
        text-align: center;
    }
</style>
<template>
  <form @submit.prevent="handleSubmit" action="">
    <label for="">Email</label>
    <input type="email" required v-model="email">
    <div v-if="emailError"  class="error">{{emailError}}</div>

    <label for="">Password</label>
    <input type="password" required v-model="password">
    <div v-if="passwordError" class="error">{{passwordError}}</div>

    <label for="">Role:</label>
    <select v-model="role">
        <option value="developer">Web Developer</option>
        <option value="designer">Web Designer</option>
        </select>

    <label>Skills</label>
    <input type="text" v-model="tempSkill" @keyup="addSkill">
    <div v-for="skill in skills" :key="skill" class="pill" @click="deleteSkill(skills.indexOf(skill))">
        {{skill}}
    </div>

        <div class="terms">
            <input type="checkbox" required v-model="terms">
            <a href="#">Accept terms and conditions</a>
        </div>
        <div class="submit">
            <button>Create an Account</button>
        </div>

  </form>


  
</template>

<script>
export default {
    data(){
        return{
            email:'',
            password:'',
            role:'',
            terms:false,
            names:[],
            tempSkill:'',
            skills:[],
            setSkills:['html','css','vue','javascript','java','python','assembly'],
            passwordError:'',
            emailError:''
        }
    },
    methods:{
        addSkill(e){
            if(e.key === 'Enter' && this.tempSkill){
                if(!this.skills.includes(this.tempSkill) &&  this.setSkills.includes(this.tempSkill)){
                    this.skills.push(this.tempSkill)
                     this.tempSkill = '' 
                }else if(!this.setSkills.includes(this.tempSkill)){
                    alert('Write a valid language:"html,css,python..."');
                }
            }
        },
        deleteSkill(e){
            this.skills.splice(e,1);
        },
        handleSubmit(){
            this.emailError = this.email.includes('@gmail.com') ? '' : 'Write a valid email!'
            this.passwordError = this.password.length>5 ? '' : 'Password must be at least 6 chars long!'
            if(!this.passwordError&& !this.emailError){
            console.log('email: ', this.email)
            console.log('password: ', this.password)
            console.log('role: ', this.role)
            console.log('skills: ', this.skills)
            console.log('terms: ', this.terms)
            }
        }
    }
}
</script>

<style>
form{
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 10px;
}
label{
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}
input, select{
    display: block;
    padding: 1*px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}
input[type="checkbox"]{
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
button{
    background: #0b6dff;
    border: 0;
    padding: 10px 20px;
    margin-top: 20px;
    color: white;
    border-radius: 20px;
}
.submit{
    text-align: center;
}
.error{
    color: #ff0062;
    margin-top: 10px;
    font-size: 0.8em;
    font-weight: bold;
}
</style>

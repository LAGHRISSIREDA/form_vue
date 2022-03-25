<template>
  <form @submit.prevent="handlSubmit">

          <label>Email :</label>
          <input type="Email" v-model="email" required>
          <label>Password :</label>
          <input type="password" v-model="password" required>
          <div v-if="passwordError" class="error">{{passwordError}}</div>
          <label>Role :</label>
          <select v-model="role">
              <option value="frontend">Developer front end</option>
              <option value="designer">Designer</option>
              <option value="backend">Developer back end</option>
          </select>

          <label >Skills :</label>
          <input type="text" @keyup.alt="addSkill" v-model="tempSkill">
          <div v-for="skill in skills" :key="skill" class="pill">
              <span @click="deleteSkill(skill)">{{skill}}</span>
          </div>

          <div class="terms">
              <input type="checkbox" required v-model="term">
              <label >Accept terms and conditions</label>
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
        role:'backend',
        term:false,
        tempSkill:'',
        skills:[],
        passwordError:''
      
    }
},
methods:{
    addSkill(e){
        if(this.tempSkill && e.key===","){
            if(!this.skills.includes(this.tempSkill)){
                this.skills.push(this.tempSkill)
            }
            this.tempSkill=''
        }
    },
    deleteSkill(skill){
        this.skills = this.skills.filter((item)=>{
            return skill !== item
        })
    },
    handlSubmit(){
        // console.log('form submited')
        // password validation
        this.passwordError = this.password>5?'':'Password Must be At least 6 chars long'
    }
}
}
</script>

<style>
form{
    box-shadow: 1px 1px 5px #0b6dff;
    max-width: 420px;
    margin: 30px auto;
    background: white;
    text-align: left;
    padding: 40px;
    border-radius: 20px;
}
label{
    color: #aaa;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 1em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}

input,select{
    display: block;
    padding: 10px 6px;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom: 1px solid #ddd;
    color: #555;
}

input[type="checkbox"]{
    display: inline-block;
    width:  16px;
    margin: 0 9px 0 0;
    position: relative;
    
}

.pill{
    display: inline-block;
    margin: 20px 20px 0 0;
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
    box-shadow: 1px 1px 10px #0b6dff;
    font-weight: bold;
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
<template>
  <!-- prevent prevents the default action of browser when form is submitted(browser refereshes the page) -->
  <form @submit.prevent="handlesubmit">
      <label>Email</label>
      <input type="email" required v-model="email">

      <label>Password</label>
      <input type="password" required v-model="password">

      <div v-if="passworderror" class="error">{{passworderror}}</div>

       <label>Role</label>
       <select v-model="role">
           <option value="developer">Web Developer</option>
           <option value="designer">Web Designer</option>

       </select>
       <label>Skills</label>
       <input type="text" v-model="tempskill" @keyup.alt="addskill"> 

       <div v-for="skill in skills" :key="skill" class="pill">
           <span @click="deleteskill(skill)">{{skill}}</span>
       </div>

       <div class="terms">
           <input type="checkbox" required v-model="terms">
           <label> * Accept terms and conditions</label>
       </div>
        <!-- <div>
           <input type="checkbox" value="snehal" v-model="names">
           <label>Snehal</label>
       </div>
        <div>
           <input type="checkbox" value="jay" v-model="names">
           <label>Jay</label>
       </div>
        <div>
           <input type="checkbox" value="dipa" v-model="names">
           <label>Dipa</label>
       </div> -->

       <div class="submit">
           <button>Create an Account</button>
       </div>
  </form>
  <!-- <p>Email : {{email}}</p>
  <p>Password : {{password}}</p>
  <p>Role : {{role}}</p>
  <p>Terms Accepted : {{terms}}</p> -->
  <!-- <p>Names : {{names}}</p> -->

</template>

<script>
export default {
    data(){
        return{
            //v-model uses the concept of two way data binding means we can have the data value from user but also we can return data value from here
            email : 'abc@gmail.com',
            password:'',
            role:'',
            terms:false,
            //names:[]
            tempskill:'',
            skills:[],
            passworderror:''
        }
    },
    methods:{
        addskill(e){
            if(e.key === ',' && this.tempskill){
                if (!this.skills.includes(this.tempskill)) {
                    this.skills.push(this.tempskill)
                }
                this.tempskill=''
            }
        },
        deleteskill(skill){
            this.skills = this.skills.filter((item) =>{
                return skill != item
            })
        },
        handlesubmit(){
            //validate password
            this.passworderror = this.password.length > 5 ? '':'Password must be at least 6 chars long'

            if (!this.passworderror) {
                console.log('Email: ',this.email)
                console.log('Password : ',this.password)
                console.log('Role: ',this.role)
                console.log('Skills: ',this.skills)
                console.log('Term accepted: ',this.terms)
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
    color: #3d3838;
    display: inline-block;
    margin: 25px 0 15px;
    font-size: 0.6em;
    text-transform: uppercase;
    letter-spacing: 1px;
    font-weight: bold;
}
input,select{
    display: block;
    padding:10px 6px ;
    width: 100%;
    box-sizing: border-box;
    border: none;
    border-bottom:1px solid #ddd ;
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
    padding: 6px,12px;
    background: #eee;
    border-radius: 20px;
    font-size: 12px;
    letter-spacing: 1px;
    font-weight: bold;
    color: #777;
    cursor: pointer;
}
button{
    background: #33cf93;
    border: 0;
    padding: 10px 20px ;
    margin-top: 20px;
    color: black;
    border-radius: 20px;

}
.submit{
    text-align: center;
}
.error{
    margin-top: 10px;
    color:#ff0062;
    font-size: 0.8em;
    font-weight: bold;
}
</style>
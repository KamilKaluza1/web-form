<template>
  <form @submit.prevent="handleSubmit">
    <label>Email:</label>
    <input type="email" v-model="email" required />

    <label>Password:{{ passwordError }}</label>
    <input type="password" v-model="password" required />

    <label>Role:</label>
    <select v-model="role">
      <option value="dev">Web Developer</option>
      <option value="des">Web Designer</option>
    </select>

    <label>Skills:</label>
    <input type="text" v-model="tempSkill" @keyup="addSkill" />
    <div v-for="skill in skills" class="pill" :key="skill" @click="deleteSkill(skill)">
      {{ skill }}
    </div>

    <div class="terms">
      <input type="checkbox" v-model="terms" />
      <label>accept terms and conditions</label>
    </div>
    <div class="submit">
        <button>Create an account</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      role: "des",
      terms: false,
      tempSkill: "",
      skills: [],
      passwordError: '',
    };
  },
  methods: {
    addSkill(e) {
      if (e.key === "," && this.tempSkill) {
        if (!this.skills.includes(this.tempSkill.slice(0, -1))) {
          this.skills.push(this.tempSkill.slice(0, -1));
        }
        this.tempSkill = "";
      }
    },
    deleteSkill(skill){
        this.skills = this.skills.filter((item)=>{item!==skill})
    },
    handleSubmit() {
      this.passwordError = this.password.length > 5 ? '' : 'minimum 6 char '
      if(!this.passwordError){
        console.log(`email: ${this.email}`)
        console.log(`password: ${this.password}`)
        console.log(`skills: ${this.skills}`)
        console.log(`terms: ${this.terms}`)
        console.log(`role: ${this.role}`)
        
      }
    }
  },
};
</script>

<style>
form {
  max-width: 400px;
  margin: 30px auto;
  background: white;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
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
input,
select {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid black;
  color: #555;
}
input[type="checkbox"] {
  display: inline-block;
  width: 16px;
  margin: 0 10px 0 0;
  position: relative;
  top: 2px;
}
.pill {
  display: inline-block;
  margin: 20px 10px 0 0;
  padding: 6px 12px;
  background: #eee;
  border-radius: 20px;
  font-size: 12px;
  letter-spacing: 1px;
  color: #777;
  font-weight: bold;
  cursor: pointer;
}
button{
    background: blue ;
    border: 0;
    padding: 10px 20px;
    margin: 20px;
    color: white;
    border-radius: 20px;
}
.submit{text-align: center;}
</style>

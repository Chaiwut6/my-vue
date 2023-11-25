<script setup>
 import {ref, computed, onMounted, watch} from 'vue'
 const isloading = ref(false)
 const isupdate = ref(false)
 const isvalid = ref(true)
 const firstname = ref('')
 const lastname = ref('')
 const email = ref('')
 const errors = ref({})

 const fullname =computed(() => {
  return `${firstname.value} ${lastname.value}`
 })

 const updateprofile = async() =>{
  isloading.value = true
  await (new Promise(resolve => setTimeout(resolve,2000)))
  isloading.value = false
  isupdate.value = true
 }

 onMounted(() =>{

 })

 watch([firstname, lastname, email], ()=>{
    isvalid.value = true
    isupdate.value = false
    errors.value = {}
    if(!validatename(firstname.value)){
      isvalid.value = false
      errors.value.firstname = 'NOT YOU'
    }
    if(!validatename(lastname.value)){
      isvalid.value = false
      errors.value.lastname = 'NOT YOU'
    }
    if(!validateemail(email.value)){
      isvalid.value = false
      errors.value.email = 'NOT email'
    }
 })

 const validatename = (name) =>{
  const re = /\d/
  return !re.test(name)
 }
 const validateemail = (email) =>{
  return email.includes('@')
 }



</script>

<template>
  <div class="Profile">
    <div class="fullname">
      <div>
        Fullname: {{ fullname }}
      </div>
       <div>
        Email: {{ email }}
       </div>
    </div>
    <div class="firstname">
      <div>Firstname:</div>
      <input type="text" v-model="firstname">
      <div class="error">{{ errors.firstname }}</div>
    </div>
    <div class="lastname">
      <div>Lastname:</div>
      <input type="text" v-model="lastname">
      <div class="error">{{ errors.lastname }}</div>
    </div>
    <div class="email">
      <div>Email:</div>
      <input type="text" v-model="email">
      <div class="error">{{ errors.email }}</div>
    </div>
    <div class="loading" v-if="isloading">
      Loading
    </div>
    <button :disabled="!isvalid" class="btn" @click="updateprofile()">Update profile</button>
    <div class="update" v-if="isupdate">
      Profile is Update
    </div>
  </div>
</template>

<style>
.Profile{
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  max-width: 320px;
  margin: 0 auto;
}
.btn{
  width: 100%;
  height: 24px;
  margin-top: 20px;
}
.Profile > div{
  width: 100%;
}
input{
  width: 100%;
}
.loading{
  background-color: beige;
  width: 100%;
  padding: 20px;
  box-sizing: border-box;
  margin: 10px 0;
}
.error{
  color: red;
}
</style>
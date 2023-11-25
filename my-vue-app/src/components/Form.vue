<script setup>
import {reactive} from 'vue'

const gendersList = ['man', 'women', 'LGBTQ']
const interestslist =['book', 'game', 'movie']
const formdata = reactive({
  interest: []
})
const submitFrom = () =>{
  console.log('formdata', formdata)
}
</script>
<template>
  <div class="register">
    <div class="fistname"><div>
      Firstname
    </div> 
      <input type="text" name="firstname" v-model="formdata.firstname">
    </div>

    <div class="lastname">
      <div>
        Lastname
      </div>
       <input type="text" name="lastname" v-model="formdata.lastname">
    </div>

    <div class="gender">
      <div>Gender</div>
      <div class="gender-for" v-for="gender in gendersList">
        <input type="radio" name="gender" :value="gender" v-model="formdata.gender"> 
        {{ gender }}
      </div>
    </div>
    <div class="interest">
        <div>Interest</div>
        <div class="interest-for" v-for="interest in interestslist">
          <input type="checkbox" name="interest" :value="interest"
          v-model="formdata.interest"> 
        {{ interest }}
        </div>
      </div>

    <div class="description">
      <div>
        Description
      </div>
      <textarea name="texarea" id="textarea" cols="25" rows="2" v-model="formdata.textare"></textarea>
    </div>
    <button @click="submitFrom()">submit</button>
  </div>
</template>
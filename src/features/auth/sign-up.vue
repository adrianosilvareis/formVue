<script>
  import { required, sameAs, email } from 'vuelidate/lib/validators'
  export default {
    mounted() {
      this.$bus.$on('navigate', this.reset)
    },
    validations: {
      username:{
        required
      },
      password:{
        required
      },
      password2:{
        required,
        sameAsPassword: sameAs('password')
      },
      email:{
        required,
        email
      }
    },
    data () {
      return {
        username: '',
        password: '',
        password2: '',
        email: ''
      }
    },
    methods: {
      submit (){
        if(!this.$v.$invalid){
          this.$emit('do-sign-up', {...this.$data})
        }else{
          this.$v.$touch()
        }
      },
      reset (selected) {
        if(selected === 'signup'){
          this.username = ''
          this.password = ''
          this.password2 = ''
          this.email = ''
          this.$v.$reset()
        }
      }
    }
  };
</script>

<template>
  <form action="#" @submit.prevent="submit" class="sign-up-htm">
    <div class="group">
      <label 
        :class="{ invalid: $v.username.$dirty && $v.username.$invalid }" 
        for="sign-up-user" 
        class="label">Username</label>
      <input
        :class="{ invalid: $v.username.$dirty && $v.username.$invalid }" 
        id="sign-up-user" 
        type="text"
        class="input"
        @input="$v.username.$touch()"
        v-model="username">
    </div>
    <div class="group">
      <label 
        for="sign-up-pass" 
        :class="{ invalid: $v.password.$dirty && $v.password.$invalid }" 
        class="label">Password</label>
      <input 
        id="sign-up-pass" 
        type="password" 
        class="input" 
        data-type="password" 
        :class="{ invalid: $v.password.$dirty && $v.password.$invalid }" 
        @input="$v.password.$touch()"
        v-model="password">
    </div>
    <div class="group">
      <label 
        for="sign-up-pass-repeat" 
        :class="{ invalid: $v.password2.$dirty && $v.password2.$invalid }" 
        class="label">Repeat Password</label>
      <input
        id="sign-up-pass-repeat" 
        type="password" 
        class="input" 
        data-type="password"
        :class="{ invalid: $v.password2.$dirty && $v.password2.$invalid }" 
        @input="$v.password2.$touch()"
        v-model="password2">
    </div>
    <div class="group">
      <label 
        for="sign-up-email" 
        :class="{ invalid: $v.email.$dirty && $v.email.$invalid }" 
        class="label">Email Address</label>
      <input 
        id="sign-up-email" 
        type="text" 
        class="input"
        :class="{ invalid: $v.email.$dirty && $v.email.$invalid }" 
        @input="$v.email.$touch()"
        v-model="email">
    </div>
    <div class="group">
      <input type="submit" class="button" value="Sign Up">
    </div>
    <div class="hr"></div>
    <div class="foot-lnk">
      <label for="tab-1">Already Member?</a></label>
    </div>
  </form>
</template>

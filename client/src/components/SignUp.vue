<template>
  <div class="hello">
    <h1>{{ msg }}</h1>

<!-- SignUp Form-->
  <form v-on:submit.prevent="signUp">
    <input type="text" v-model="email" placeholder="Email">
    <input type="text" v-model="firstName" placeholder='First Name'>
    <input type="text" v-model="lastName" placeholder="Last Name">
    <input type="password" v-model="password" placeholder="Password">
    <input type="password" v-model="password2" placeholder="Confirm Password">
    <button type="submit">SignUp</button>
  </form>

  </div>
</template>

<script>
import gql from 'graphql-tag'

export default {
  name: 'SignUp',
  // eslint-disable-next-line
  data() {
    return {
      msg: 'Welcome to BizLoop',
      email: '',
      firstName: '',
      lastName: '',
      password: '',
      password2: ''
    }
  },

  computed: {
    // eslint-disable-next-line
    name: function() {
      return this.firstName + ' ' + this.lastName
    }
  },

  methods: {
    // eslint-disable-next-line
    signUp: function(event) {
      this.$apollo.mutate({
        mutation: gql`
          mutation($email: String!, $password: String!, $name: String!) {
            signup(email: $email, password: $password, name: $name){}
          }
        `,
        variables: {
          name: this.name,
          password: this.password,
          email: this.email
        }
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
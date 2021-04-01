<template>
  <div id="app">
    <UserForm />
    <UserAddress />
    <UserPassport />
  </div>
</template>

<script>
  import UserForm from "@/components/UserForm";
  import UserAddress from "@/components/UserAddress";
  import UserPassport from "@/components/UserPassport";

export default {
  name: 'App',
  components: {
    UserPassport,
    UserAddress,
    UserForm
  }
}
</script>

<style lang="sass">
#app
  font-family: Roboto, 'sans-serif'
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  display: flex
  justify-content: space-evenly
  color: #2c3e50
  margin-top: 60px
  flex-wrap: wrap

@media only screen and (max-width: 1008px)
  #app
    /*align-items: center*/
    /*flex-direction: column*/
</style>

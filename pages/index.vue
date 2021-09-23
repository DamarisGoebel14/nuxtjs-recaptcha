<template>
  <div>
    <h1>Hello</h1>
    <form @submit.prevent="onSubmit">
      <input autocomplete="true" placeholder="Email" type="email" v-model="email">
      <input autocomplete="current-password" placeholder="Password" type="password" v-model="password">
      <recaptcha/>
      <button type="submit">Sign In</button>
    </form>
  </div>
</template>

<script>
export default {
  methods: {
    async onSubmit() {
      try {
        const token = await this.$recaptcha.getResponse()
        console.log('ReCaptcha token:', token)

        // send token to server alongside your form data

        // at the end you need to reset recaptcha
        await this.$recaptcha.reset()
      } catch (error) {
        console.log('Login error:', error)
      }
    },
  }
}
</script>

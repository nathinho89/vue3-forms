<template>
  <form @submit.prevent="onSubmit">
    <BaseInput
      label="Email"
      type="email"
      v-model="email"
      :error="emailError"
    />

    <BaseInput
      label="Password"
      type="password"
      v-model="password"
      :error="passwordError"
    />

    <BaseButton
      type="submit"
      class="-fill-gradient"
    >
    Submit
    </BaseButton>
  </form>
</template>

<script>
import { useField, useForm } from 'vee-validate'

export default {
  setup () {
    function onSubmit () {
      alert('Submitted')
    }

    const validations = {
      email: value => {
        if (!value || value === null || value === undefined || !String(value).length) return 'This field is required'

        const regex = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/
        if (!regex.test(String(value).toLowerCase())) {
          return 'Please enter a valid email address'
        }

        return true
      },
      password: value => {
        if (!value || value === null || value === undefined || !String(value).length) return 'This field is required'
        return true
      }
    }

    useForm({
      validationSchema: validations
    })

    const { value: email, errorMessage: emailError } = useField('email')
    const { value: password, errorMessage: passwordError } = useField('password')

    return {
      onSubmit,
      email: email,
      emailError: emailError,
      password: password,
      passwordError: passwordError
    }
  }
}
</script>

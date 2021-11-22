<template>
  <form @submit.prevent="onSubmit">
    <BaseInput
      label="Email"
      type="email"
      :error="emailError"
      :modelValue="email"
      @change="handleChange"
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

    const { setFieldValue } = useForm({
      validationSchema: validations
    })

    const { value: email, errorMessage: emailError } = useField('email')
    const { value: password, errorMessage: passwordError } = useField('password')

    const handleChange = (event) => {
      setFieldValue('email', event.target.value)
    }

    return {
      onSubmit,
      email,
      emailError,
      password,
      passwordError,
      handleChange // applies lazy validation onChange (when not focused)
    }
  }
}
</script>

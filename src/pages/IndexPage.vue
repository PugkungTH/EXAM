<template>
  <q-page class="flex flex-center">
    <q-form class="q-pa-md" @submit="onSubmit" @reset="onReset" style="width: 400px">
      <q-input filled v-model="name" label="Your name" lazy-rules :rules="[ val => val && val.length > 0 || 'Please type something']" />
      <q-input filled type="number" v-model="age" label="Your age" lazy-rules :rules="[ val => val > 0 || 'Please type your age']" />
      <q-toggle v-model="accept" label="I accept the license and terms" />
      <div class="q-mt-md">
        <q-btn label="Submit" type="submit" color="primary" />
        <q-btn label="Reset" type="reset" flat class="q-ml-sm" />
      </div>
    </q-form>
  </q-page>
</template>

<script setup>
import { ref } from 'vue'
import { Notify } from 'quasar'

const name = ref('')
const age = ref(null)
const accept = ref(false)

function onSubmit() {
  if (!accept.value) {
    Notify.create('Please accept the terms first.')
    return
  }
  Notify.create(`Submitted! Name: ${name.value}, Age: ${age.value}`)
}
function onReset() {
  name.value = ''
  age.value = null
  accept.value = false
}
</script>

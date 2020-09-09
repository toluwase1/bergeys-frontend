<template>
  <v-alert type="error">
    {{ message }}
  </v-alert>
</template>

<script>
export default {
  name: 'Notification',
  props: ['message']
}
</script>
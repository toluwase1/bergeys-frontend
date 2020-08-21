<template>
<div>
    <h1>This is the error page</h1>
    <h1> {{error.statusCode}} not Found</h1>
</div>
</template>

<script>
export default {
    layout:'error-layout',
    props: {
    error: {
      type: Object,
      default: null
    }
  },
}
</script>

<style>

</style>
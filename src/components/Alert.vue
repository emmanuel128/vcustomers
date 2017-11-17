<template lang="pug">
  div(role="alert").alert.alert-warning.alert-dismissible {{message}}
    button(type="button", data-dismiss="alert", aria-label="Close").close 
      span(aria-hidden="true") &times;
    
</template>

<!--
<template>
  <div class="alert alert-warning alert-dismissible" role="alert">
    <button type="button" class="close" data-dismiss="alert" aria-label="Close"><span aria-hidden="true">&times;</span></button>
      {{message}}
  </div>
</template>
-->

<script>
export default {
  name: 'alert',
  props: ['message'],
  data () {
    return {
      
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>

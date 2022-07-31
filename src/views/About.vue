<template>
  <div class="about">
    <h1>This is an about page</h1>
    <hello-dialog-vue></hello-dialog-vue>

  </div>
</template>

<script>
import HelloDialogVue from '../components/HelloDialog.vue'
export default {
  name: 'About',

  data () {
    return {}
  },
  components: {
    HelloDialogVue
  }

}

</script>

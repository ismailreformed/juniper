<template>
  <div>
    <Navbar />
    <br>
    <b-container>
      <ContentBody />
    </b-container>
  </div>
</template>

<script>
import Navbar from '~/components/Navbar.vue'
import ContentBody from '~/components/ContentBody.vue'

export default {
  components: {
    Navbar,
    ContentBody
  }
}
</script>

<style>
</style>

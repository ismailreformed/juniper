<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="info">
      <b-navbar-brand href="#">
        <!-- <b-img
          width="175"
          height="55"
          :src="logo"
          fluid
          alt="Responsive image"
        /> -->
        <h3>JUNIPER <span>|</span> Release Content </h3>
      </b-navbar-brand>

      <b-navbar-toggle target="nav-collapse" />

      <b-collapse id="nav-collapse" is-nav>
        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">
          <b-nav-form>
            <div>
              <b-button pill variant="outline-secondary">
                help
              </b-button>
            </div>
          </b-nav-form>
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>
  </div>
</template>
<script>
import logo from '~/assets/image/juniperLogo.jpg'
export default {
  data () {
    return {
      logo
    }
  }
}
</script>

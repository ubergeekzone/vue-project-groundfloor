<template>
  <b-navbar class="gf-navbar" type="dark" variant="dark"
            toggleable="md">

    <b-navbar-brand href="#">
      <img class="gf-header-brand" src="~/assets/GROUNDFLOOR-light-text.png">
    </b-navbar-brand>

    <b-collapse id="nav_collapse" is-nav>

      <!-- <b-navbar-nav>
           <b-nav-item href="#">Investing</b-nav-item>
           <b-nav-item href="#" disabled></b-nav-item>
           </b-navbar-nav> -->

      <!-- Right aligned nav items -->
      <b-navbar-nav class="ml-auto">

        <b-nav-item-dropdown text="INVEST" right>
          <b-dropdown-item href="#">FUNDING</b-dropdown-item>
          <b-dropdown-item href="#">FUNDED</b-dropdown-item>
        </b-nav-item-dropdown>

        <b-nav-item>BORROW</b-nav-item>

      </b-navbar-nav>

    </b-collapse>
  </b-navbar>
</template>

<script>
export default {
  beforeAsync() {
    console.log('stuff')
  }
}
</script>

<style>
img.gf-header-brand {
  height: 2em;
}
</style>

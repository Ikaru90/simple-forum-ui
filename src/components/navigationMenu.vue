<template>
  <div class="row">
    <div class="col menu-text">
      <ul v-if="user" class="nav justify-content-end">
        <li class="nav-item">
          <a class="nav-link active" href="/" data-toggle="modal" data-target="#theme-modal">New theme</a>
        </li>
        <li class="nav-item">
          <a class="nav-link active" href="/" data-toggle="modal" data-target="#profile-modal">{{ user.username }}</a>
        </li>
        <li class="nav-item">
          <a class="nav-link active" href="/" @click="onLogout">Log out</a>
        </li>
      </ul>
      <ul v-else class="nav justify-content-end">
        <li class="nav-item">
          <a class="nav-link active" href="/" data-toggle="modal" data-target="#signup-modal">Sign up</a>
        </li>
        <li class="nav-item">
          <a class="nav-link active" href="/" data-toggle="modal" data-target="#login-modal">Log in</a>
        </li>  
      </ul>
    </div>
    <LoginModal v-bind:onLogin="onLogin" />
    <SignupModal v-bind:onSignup="onSignup" />
    <ProfileModal v-bind:user="user" />
    <ThemeModal />
  </div>
</template>

<script>
import login from './modals/login';
import signup from './modals/signup';
import profile from './modals/profile';
import theme from './modals/theme';

export default {
  name: 'navigationMenu',
  props: [
    'user',
    'onSignup',
    'onLogin',
    'onLogout'
  ],
  components: {
    "LoginModal": login,
    "SignupModal": signup,
    "ProfileModal": profile,
    "ThemeModal": theme,
  }
}
</script>

<style>
  .menu-text {
    font-size: 30px;
    color: black !important;
  }
</style>
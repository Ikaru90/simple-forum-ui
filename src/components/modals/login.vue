<template>
  <div class="modal fade" id="login-modal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">Log In</h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <div class="modal-body">
          <form @submit="handleLogin">
            <div v-if="error" class="error">{{ error }}</div>
            <div class="form-group">
              <label for="username"><b>Username</b></label>
              <input required type="text" class="form-control" id="username" v-model="username" placeholder="Enter Username" autocomplete="off">
            </div>
            <div class="form-group">
              <label for="password"><b>Password</b></label>
              <input required type="password" class="form-control" id="password" v-model="password" placeholder="Password">
            </div>
            <button type="submit" class="btn btn-block btn-primary">Log in</button>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import $ from 'jquery';
import { api } from 'utils/api';

export default {
  name: 'login',
  data() {
    return {
      error: null,
      username: null,
      password: null,
    }
  },
  props: ['onLogin'],
  methods: {
    handleLogin(e) {
      e.preventDefault();
      e.stopPropagation();

      const data = {
        username: this.username,
        password: this.password,
      }

      api.POST('/api/auth/login', data).then((result) => {
        if (result.data && result.data.username) {
          this.$notify({
            group: 'auth',
            type: 'success',
            text: 'Login successfully'
          });

          this.onLogin(result.data);
          $('#login-modal').modal('hide');

          this.username = null;
          this.password = null;
          this.error = null;
        }
      }).catch((error) => {
        this.error = error.response.data.errorMessage;
        this.password = null;
      });
    },
  }
}
</script>
<template>
  <div>
    <b-container>
      <br>
      <br>
      <br>
      <br>
      <b-row align-content="center">
        <b-col align-self="start" cols="3" />
        <b-col align-self="center" cols="6">
          <b-card-group deck>
            <b-card header-tag="header" body-class="text-center">
              <b-card-text>
                <h6 class="mb-0">
                  Disk Stats
                </h6>
                <span>---------</span>
                <br>
                <div>
                  <b-form @submit="onSubmit" @reset="onReset">
                    <b-form-group
                      id="input-group-1"
                      label="Username:"
                      label-for="input-1"
                    >
                      <b-form-input
                        id="input-1"
                        v-model="username"
                        type="text"
                        required
                        placeholder="Enter Username"
                      />
                    </b-form-group>

                    <b-form-group id="input-group-2" label="Password:" label-for="input-2">
                      <b-form-input
                        id="input-2"
                        v-model="password"
                        required
                        placeholder="Enter name"
                      />
                    </b-form-group>

                    <b-button type="submit" variant="primary">
                      Login
                    </b-button>
                    <b-button type="reset" variant="danger">
                      Reset
                    </b-button>
                  </b-form>
                </div>
              </b-card-text>
            </b-card>
          </b-card-group>
        </b-col>
        <b-col align-self="start" cols="3" />
      </b-row>
    </b-container>
  </div>
</template>
<script>
export default {
  data () {
    return {
      password: '',
      username: ''
    }
  }
}
</script>

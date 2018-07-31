<template>
  <div class="container">
    <form>
      <div class="row">
        <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
            <h1>File a Complaint</h1>
            <hr>
            <div class="form-group">
              <label for="email">Email</label>
              <input type="text" class="form-control" name="email" id="email" :value="userData.email" @input="userData.email = $event.target.value">
            </div>
            <div class="form-group">
              <label for="password">Password</label>
              <input type="password" class="form-control" name="password" id="password" v-model.lazy="userData.password">
            </div>
            <div class="form-group">
              <label for="age">Age</label>
              <input type="text" class="form-control" name="age" id="age" v-model.number="userData.age">
            </div>
        </div>
      </div>
      <div class="row">
        <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
          <div class="form-group">
            <label for="message">Message</label>
            <textarea name="message" id="message" rows="5" class="form-control" v-model="message"></textarea>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
          <div class="form-group">
            <label for="sendmail" class="checkbox-inline">
              <input type="checkbox" value="sendmail" id="sendmail" v-model="sendMail"> Send Mail
            </label>
            <label for="sendinfomail" class="checkbox-inline">
              <input type="checkbox" value="sendinfomail" id="sendinfomail" v-model="sendMail"> Send Info Mail
            </label>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
          <div class="form-group">
            <input type="radio" name="male" value="male" id="male" v-model="gender">
            <label for="male">Male</label>
            <input type="radio" name="female" value="female" id="female" v-model="gender">
            <label for="female">Female</label>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
          <div class="form-group">
            <label for="priority">Priority</label>
            <select class="form-control" name="priority" id="priority" v-model="selectedPriority">
              <option value="default" selected>---- Choose The Priority Level ---</option>
              <option v-for="item in priority">{{ item }}</option>
            </select>
          </div>
        </div>
      </div>
      <!-- Bisa menggunakan emit biasa tapi bisa juga menggunakan langsung emit input -->
      <div class="row">
        <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
          <appSwitch v-model="dataSwitch"></appSwitch>
        </div>
      </div>
      <hr>
      <div class="row">
        <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
          <button class="btn btn-primary" @click.prevent="submitted">Submit!</button>
        </div>
      </div>
      <hr>
    </form>
    <div class="row" v-if="isSubmitted">
      <div class="col-xs-12 col-sm-8 col-sm-offset-2 col-md-6 col-md-offset-3">
        <div class="panel panel-default">
          <div class="panel-heading">
            <h4>Your Data</h4>
          </div>
          <div class="panel-body">
            <p>Mail : {{ userData.email }} </p>
            <p>Password : {{ userData.password }} </p>
            <p>Age : {{ userData.age }} </p>
            <p style="white-space: pre">Message : {{ message }}</p>
            <p><strong>Send Mail ?</strong></p>
            <ul>
              <li v-for="item in sendMail">{{ item }}</li>
            </ul>
            <p>Gender : {{ gender }}</p>
            <p>Priority : {{ selectedPriority }}</p>
            <p>Switched : {{ dataSwitch }} </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Switch from './components/Switch.vue'

export default {
  data() {
    return {
      userData: {
        email: '',
        password: '',
        age: 0,
      },
      message: 'A New Text',
      sendMail: [],
      gender: 'male',
      priority: ['High', 'Medium', 'Low'],
      selectedPriority: 'High',
      dataSwitch: true,
      isSubmitted: false
    }
  },
  components: {
    appSwitch: Switch
  },
  methods: {
    switched(value) {
      if (value == true) {
        this.dataSwitch = true
      } else if (value == false) {
        this.dataSwitch = false
      }
    },
    submitted() {
      this.isSubmitted = true
    }
  }
}
</script>

<style>
</style>

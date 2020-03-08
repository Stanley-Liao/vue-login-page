<template>
    <div id="app">
        <div class="main-body">
            <div class="header">
                <h3 class="h3-title">Choose Account Type</h3>
            </div>
            <div class="menu">
              
                <div v-for="(role, key) in roles" class="actype-item cp" :class="{'actype-item-selected': role.selected}" @click="changeType(key)">
                    <div>
                        <component :is="role.type" class="svg-item"></component>
                        <!-- <DoctorSvg class="svg-item" /> -->
                    </div>
                    <div class="actype-text">{{ role.name }}</div>
                    <SelectedSvg v-show="role.selected" class="selected-svg" />
                </div>         

            </div>
            <div class="desc">
                <p>Hello {{ currentRole }}!</p>
                <p>Please fill out the form below to get start</p>
            </div>
            <div class="content">
                <div class="form">
                    <CsInput v-model="username" placeholder="Username">
                        <EmailSvg slot="icon" />

                    </CsInput>
                    <CsInput v-model="password" placeholder="Password">
                        <LockSvg slot="icon" />
                        <span slot="addon" class="forgot"><a :href="forgotUrl">Forgot?</a></span>
                    </CsInput>          
                    <div class="form-footer">
                        <span class="signup-box">
                            No account? 
                            <span class="signup cp">
                                <a :href="forgotUrl">Signup</a>
                            </span>
                        </span>
                        <button class="btn login-box" @click="clickLogin">Login</button>
                    </div>
                </div> 
              </div>
              <div class="footer">
                  <TownSvg/>
              </div>
        </div>
    </div>
</template>

<script>
import DoctorSvg from './components/DoctorSvg.vue'
import PatientSvg from './components/PatientSvg.vue'
import TownSvg from './components/TownSvg.vue'
import SelectedSvg from './components/SelectedSvg.vue'
import EmailSvg from './components/EmailSvg.vue'
import CsInput from './components/CsInput.vue'
import LockSvg from './components/LockSvg.vue'
import styles from './assets/sass/main.scss' 

export default {
  name: 'App',
  components: {
      DoctorSvg,
      PatientSvg,
      TownSvg,
      SelectedSvg,
      EmailSvg,
      CsInput,
      LockSvg
  },
  data(){
      return {
          roles: [
              {name: 'doctor', type: 'DoctorSvg', selected: true}, 
              {name: 'patient', type: 'PatientSvg', selected: false}
          ],
          username: '',
          password: '',
          forgotUrl: 'http://localhost:8080/forgot',
          signupUrl: 'http://localhost:8080/signup'
      }
  },
  computed:{
      currentRole(){
          let role = this.roles.find( (obj) => obj.selected === true)
          if(role) return role.name
          else return ''
      }
  },
  methods:{
      clickLogin(){

          this.login(this.username, this.password).then((res) => {

              if(res === true){

                  alert('通過')
              }else{

                  alert('不通過')
              }
          })
      },
      login(username, password){
          return new Promise((resolve, reject)=>{

              if(username === 'abc12345' && password === 'c124345ksfh'){

                  resolve(true)
              }else{

                  resolve(false)
              }
          })
      },
      changeType(key){

          let removeTarget = this.roles.find((obj) => obj.selected == true )
          if(removeTarget){

              removeTarget.selected = false
              this.roles[key].selected = true
          }

      }
  }
}
</script>

<template>
  <div>

  
  <section
    class="vh-100 bg-image ">
    <div class="mask d-flex align-items-center h-100 gradient-custom-3">
      <div class="container h-100">
        <div class="row d-flex justify-content-center align-items-center h-100">
          <div class="col-12 col-md-9 col-lg-7 col-xl-6">
            <div class="card" style="border-radius: 15px">
              <div class="card-body p-5">
                <h2 class="text-uppercase text-center mb-5">
                  Create an account
                </h2>

                <form @click.prevent>
                  <div class="form-outline mb-4">
                    <input
                      type="text"
                      id="form3Example1cg"
                      v-model="state.name"
                      class="form-control form-control-lg"  :class="{ error: v$.name.$errors.length }"
                    />
                    <label class="form-label" for="form3Example1cg"
                      >Your Name</label
                    >
                  </div>
                  <!-- errors -->
                  <div class="input-errors" v-for="error of v$.name.$errors" :key="error.$uid">
                    <div class="error-msg">{{ error.$message }}</div>
                </div>
                  <!-- end errors -->
                  <div class="form-outline mb-4">
                    <input
                      type="email"
                      v-model="state.email"
                      id="form3Example3cg"
                      class="form-control form-control-lg"
                    />
                    <label class="form-label" for="form3Example3cg"
                      >Your Email</label
                    >
                  </div>
                   <!-- errors -->
                   <div class="input-errors" v-for="error of v$.email.$errors" :key="error.$uid">
                    <div class="error-msg">{{ error.$message }}</div>
                </div>
                  <!-- end errors -->

                  <div class="form-outline mb-4" >
                    <input
                      type="password"
                      v-model="state.password"
                      id="form3Example4cg"
                      class="form-control form-control-lg"
                    />
                    <label class="form-label" for="form3Example4cg"
                      >Password</label
                    >
                  </div>
                    <!-- errors -->
                    <div class="input-errors" v-for="error of v$.password.$errors" :key="error.$uid">
                    <div class="error-msg">{{ error.$message }}</div>
                </div>
                  <!-- end errors -->

                  <div class="form-outline mb-4">
                    <input
                      type="password"
                      v-model="state.confirm_password"
                      id="form3Example4cdg"
                      class="form-control form-control-lg"
                    />
                    <label class="form-label" for="form3Example4cdg"
                      >Repeat your password</label
                    >
                  </div>
                    <!-- errors -->
                    <div class="input-errors" v-for="error of v$.confirm_password.$errors" :key="error.$uid">
                    <div class="error-msg">{{ error.$message }}</div>
                </div>
                  <!-- end errors -->

                  <div class="form-check d-flex justify-content-center mb-5">
                    <input
                      class="form-check-input me-2"
                      type="checkbox"
                      value=""
                      id="form2Example3cg"
                    />
                    <label class="form-check-label" for="form2Example3g">
                      I agree all statements in
                      <a href="#!" class="text-body"><u>Terms of service</u></a>
                    </label>
                  </div>

                  <div class="d-flex justify-content-center">
                    <button
                      type="submit"
                      class="btn btn-success btn-block btn-lg gradient-custom-4 text-body"
                      @click="signUp()"
                    >
                      Register
                    </button>
                  </div>

                  <p class="text-center text-muted mt-5 mb-0">
                    Have already an account?
                    <button class="fw-bold text-body btn btn-link" @click="redirectTo({val : 'login'})"><u>Login here</u></button>
                  </p>
                </form>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
  </div>
</template>

<script>
import { reactive } from 'vue';
import { mapActions } from 'vuex';
import { useVuelidate } from '@vuelidate/core';
import { required, email ,minLength,sameAs} from '@vuelidate/validators';
import { computed } from 'vue';

export default {
  setup () {
    const  state = reactive({
      name:"",
      email:"",
      password:"",
      confirm_password:"",

    })
    const rules=computed ((() =>{
      return {
        name: { required,minLength:minLength(5)},
        email: { required, email },
        password:{ required, minLength:minLength(9)},
        confirm_password:{ required , sameAsPassword: sameAs(state.password),},
      };
     
    
  }))
    const v$ = useVuelidate(rules, state)
    return { state, v$ }
  },
  
  
  methods: {
    ...mapActions(['redirectTo']),
    signUp(){
      this.v$.$validate();
      if(!this.v$.$errors){
        console.log('yes');
      }
      else{
        console.log('no');
      }
     
    }
  },
};
</script>

<style lang="scss" scoped>
.gradient-custom-3 {
  /* fallback for old browsers */
  background: #84fab0;

  /* Chrome 10-25, Safari 5.1-6 */
  background: -webkit-linear-gradient(
    to right,
    rgba(132, 250, 176, 0.5),
    rgba(143, 211, 244, 0.5)
  );

  /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  background: linear-gradient(
    to right,
    rgba(132, 250, 176, 0.5),
    rgba(143, 211, 244, 0.5)
  );
}
.bg-image{
  background-image: url('https://mdbcdn.b-cdn.net/img/Photos/new-templates/search-box/img4.webp');

}
.gradient-custom-4 {
  /* fallback for old browsers */
  background: #84fab0;

  /* Chrome 10-25, Safari 5.1-6 */
  background: -webkit-linear-gradient(
    to right,
    rgba(132, 250, 176, 1),
    rgba(143, 211, 244, 1)
  );

  /* W3C, IE 10+/ Edge, Firefox 16+, Chrome 26+, Opera 12+, Safari 7+ */
  background: linear-gradient(
    to right,
    rgba(132, 250, 176, 1),
    rgba(143, 211, 244, 1)
  );
}
</style>

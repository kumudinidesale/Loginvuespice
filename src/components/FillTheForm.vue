<template>
  <v-app id="inspire" class="pa-10">
    <v-row justify="center">
      <v-card class="pa-10" height="550" width="500">
        <form @submit.prevent="update">
          <h1 style="text-align: center">SingIn</h1>
          <v-text-field v-model.trim="input.name" label="Fname"></v-text-field>
          <div class="req" v-if="!$v.input.name.required">Name is required</div>
          <div class="req" v-if="!$v.input.name.minLength">
            Name must have at least
            {{ $v.input.name.$params.minLength.min }} letters.
          </div>

          <v-text-field v-model.trim="input.email" label="Email"></v-text-field>
          <div class="req" v-if="!$v.input.email.required">
            Email is required
          </div>
          <div class="req" v-if="!$v.input.email.minLength">
            Email must have at least
            {{ $v.input.email.$params.minLength.min }} letters.
          </div>

          <v-text-field v-model="input.phoneno" label="Phoneno"></v-text-field>
          <div class="req" v-if="!$v.input.phoneno.required">
            PhoneNo is required
          </div>
          <div class="req" v-if="!$v.input.phoneno.minLength">
            PhoneNo must have at Number
            {{ $v.input.phoneno.$params.minLength.min }} letters.
          </div>

          <v-select
            :items="statename"
            v-model="input.state"
            label="State"
            required
          ></v-select>
          <div class="req" v-if="!$v.input.state.required">
            State is required
          </div>

          <v-btn
            class="mr-4"
            @click="update"
            type="update"
            :disabled="this.$v.$invalid || submitStatus === 'PENDING'"
          >
            submit
          </v-btn>
          <p class="typo__p" v-if="submitStatus === 'OK'">
            Thanks for your submission!
          </p>
          <p class="typo__p" v-if="submitStatus === 'ERROR'">
            Please fill the form correctly.
          </p>
          <p class="typo__p" v-if="submitStatus === 'PENDING'">Sending...</p>
        </form>
      </v-card>
    </v-row>
  </v-app>
</template>
  <script>
import { required, minLength } from "vuelidate/lib/validators";
export default {
  name: "FillTheForm",
  validations: {
    input: {
      name: {
        required,
        minLength: minLength(4),
      },
      email: {
        required,
        minLength: minLength(5),
      },

      phoneno: {
        required,
        minLength: minLength(9),
      },
      state: {
        required,
        minLength: minLength(2),
      },
    },
  },

  data() {
    return {
      statename: ["Maharashtra", "Gujrat", "Panjab", "Karnataka"],
      input: {
        name: "",
        email: "",
        phoneno: "",
        state: "",
        submitStatus: null,
      },
    };
  },

  methods: {
    update() {
      this.$emit("input", this.input);
      console.log("update!");
      this.$v.$touch();
      if (this.$v.$invalid) {
        this.submitStatus = "ERROR";
      } else {
        // do your submit logic here
        this.submitStatus = "PENDING";
        setTimeout(() => {
          this.submitStatus = "OK";
        }, 500);
      }
    },
  },
};
</script>
  
  <style>
.req {
  color: red;
  font-size: 10px;
}
</style>
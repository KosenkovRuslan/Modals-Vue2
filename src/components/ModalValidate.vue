<template>
  <modal title="Modal with form + validate" @close="$emit('close')">
    <div slot="body">
      <form @submit.prevent="onSubmit">
        <!-- Name -->
        <div class="form-item" :class="{ errorInput: $v.name.$error }">
          <label>Name:</label>
          <p class="errorText" v-if="!$v.name.required">Field is required!</p>
          <p class="errorText" v-if="!$v.name.minLength">
            Name must have at least {{ $v.name.$params.minLength.min }}!
          </p>
          <input
            v-model="name"
            :class="{ error: $v.name.$error }"
            @change="$v.name.$touch"
          />
        </div>

        <!-- Password -->
        <div class="form-item" :class="{ errorInput: $v.password.$error }">
          <label>Password</label>
          <p class="errorText" v-if="!$v.password.required">Password is required</p>
          <p class="errorText" v-if="!$v.password.minLength">password must have at least {{ $v.password.$params.minLength.min }}!</p>
          <input
            type="password"
            v-model="password"
            :class="{ error: $v.password.$error }"
            @change="$v.password.$touch"
          />
        </div>

        <!-- Confirm password -->
        <div class="form-item" :class="{ errorInput: $v.confirmPassword.$error }">
          <label>Confirm password</label>
          <p class="errorText" v-if="!$v.confirmPassword.required">Confirm password is required</p>
          <p class="errorText" v-if="!$v.confirmPassword.sameAsPassword">The field value must match the password field</p>
          <input
            type="password"
            v-model="confirmPassword"
            :class="{ error: $v.confirmPassword.$error }"
            @change="$v.confirmPassword.$touch"
          />
        </div>

        <!-- Email -->
        <div class="form-item" :class="{ errorInput: $v.email.$error }">
          <label>Email:</label>
          <p class="errorText" v-if="!$v.email.required">Field is required!</p>
          <p class="errorText" v-if="!$v.email.email">Email novalid!</p>
          <input
            v-model="email"
            :class="{ error: $v.email.$error }"
            @change="$v.email.$touch()"
          />
        </div>

        <!-- Button submit -->
        <button class="btn btnPrimary">Submit</button>
      </form>
    </div>
  </modal>
</template>

<script>
import { required, minLength, email, sameAs } from 'vuelidate/lib/validators'
import modal from '@/components/UI/Modal.vue'
export default {
  components: {
    modal,
  },
  data() {
    return {
      name: '',
      password: '',
      confirmPassword: '',
      email: '',
    }
  },

  validations: {
    name: {
      required,
      minLength: minLength(4),
    },
    password: {
      required,
      minLength: minLength(6)
    },
    confirmPassword: {
      required,
      sameAsPassword: sameAs('password')
    },
    email: {
      required,
      email,
    },
  },

  methods: {
    onSubmit() {
      this.$v.$touch()
      if (!this.$v.$invalid) {
        const user = {
          name: this.name,
          email: this.email,
          password: this.password
        }

        console.log(user)

        // Done
        this.name = ''
        this.email = ''
        this.password = ''
        this.confirmPassword = ''
        this.$v.$reset()
        this.$emit('close')
      }
    },
  },
}
</script>

<style lang="scss">
.form-item .errorText {
  display: none;
  margin-bottom: 8px;
  font-size: 13px;
  color: rgb(206, 17, 17);
}

.form-item {
  &.errorInput .errorText {
    display: block;
  }
}

input.error {
  border-color: rgb(206, 17, 17);
}
</style>

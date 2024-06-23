<template>
  <div class="dark-mode d-flex justify-content-center align-items-center ">
    <b-form @submit="onSubmit" @reset="onReset" v-if="show" class="p-4 rounded shadow-lg" style="max-width: 400px; width: 100%; background:#333">
      <b-form-group
        id="input-group-1"
        label="Email address:"
        label-for="input-1"
        class="mb-3"
      >
        <b-form-input
          id="input-1"
          v-model="form.email"
          type="email"
          placeholder="Enter email"
          required
        ></b-form-input>
      </b-form-group>

      <b-form-group
        id="input-group-2"
        label="Password:"
        label-for="input-2"
        class="mb-3"
      >
        <b-form-input
          id="input-2"
          v-model="form.password"
          placeholder="Enter your password"
          required
        ></b-form-input>
      </b-form-group>

      <b-button type="submit" variant="primary" @click="register()" class="mb-3">Submit</b-button>
    </b-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        email: '',
        password: ''
      },
      show: true
    };
  },
  methods: {
    register(){
      axios.post('/register/registration',this.form).then(response=>{
        console.log(response.data.email);
        console.log(response.data.password);
      }).catch(error=>{
        console.log(error.data);
        this.loading = false;
      })
    },
    onSubmit(event) {
      event.preventDefault();
      alert(JSON.stringify(this.form));
    },
    onReset(event) {
      event.preventDefault();
      this.form.email = '';
      this.form.password = '';
      this.show = false;
      this.$nextTick(() => {
        this.show = true;
      }); 
    }
  }
};
</script>

<style scoped>
.dark-mode {
  color: #fff; /* Light text color */
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.dark-mode b-form-group {
  color: #fff; /* Light text color for form labels */
}

.dark-mode b-button {
  background-color: #007bff; /* Primary button color */
}

.dark-mode b-button:hover {
  background-color: #0056b3; /* Darker hover color */
}

.dark-mode b-form-input,
.dark-mode b-form-textarea {
  background-color: #444; /* Dark input background color */
  color: #fff; /* Light text color for inputs */
  border-color: #666; /* Dark border color */
}
</style>

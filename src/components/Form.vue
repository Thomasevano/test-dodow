<template>
  <div role="group">
    <label for="input-live">Name:</label>
    <b-form-input
      id="input-live"
      v-model="name"
      :state="nameState"
      aria-describedby="input-live-help input-live-feedback"
      placeholder="Enter your name"
      trim
    ></b-form-input>

    <!-- This will only be shown if the preceding input has an invalid state -->
    <b-form-invalid-feedback id="input-live-feedback">
      Enter at least 3 letters
    </b-form-invalid-feedback>

    <!-- This is a form text block (formerly known as help block) -->
    <b-form-text id="input-live-help">Your full name.</b-form-text>

    <label for="city">Ville</label>
    <b-form-input
      id="city"
      v-model="city"
      type="text"
      placeholder="Entrer une vile"
      name="city"
    ></b-form-input>
    <label for="zipcode">code postal</label>
    <b-form-input
      id="zipcode"
      v-model="zipcode"
      :state="zipcodeValidation"
      placeholder="Enter a correct zipcode: ***-****"
      name="zipcode"
      type="text"
    ></b-form-input>
  </div>
</template>

<script>
  export default {
    computed: {
      nameState() {
        return name.length > 2 ? true : false
      },
      zipcodeValidation() {
        return (this.validZipcode(this.zipcode)) ? true : false;
      }
    },
    data() {
      return {
        name: '',
        city: '',
        zipcode: '',
        // if (zipcode.length === 3){
        //   return zipcode: this.zipcode.value + '-';
        // }
        }
    },
    methods: {
    checkForm: function (e) {
      this.errors = [];

      if (!this.city) {
        this.errors.push("Vous devez entrer une ville.");
      }
      else if(this.validCity(this.city)) {
        this.errors.push('Entrer une ville valide.');
      }
      if (!this.zipcode) {
        this.errors.push('Vous devez entrer un code postal.');
      }
      else if (!this.validZipcode(this.zipcode)) {
        this.errors.push('Valid zipcode required.');
      }

      if (!this.errors.length) {
        return true;
      }

      e.preventDefault();
    },
    validZipcode: function (zipcode) {
      var re = /^\d{3}(?:[-]\d{4})?$/;
      return re.test(zipcode);
    },
    validCity: function(city) {
      var re = /[a-zA-Z0-9_]*$/;
      return re.test(city);
    }
    }
  }
</script>
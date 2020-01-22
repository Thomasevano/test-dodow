<template>
  <form role="group"
  @submit="checkForm"
  >

  <p v-if="errors.length">
    <b>Veuillez corriger les erreurs suivantes</b>
    <ul>
      <li v-for="error in errors" :key="error">{{ error }}</li>
    </ul>
  </p>

    <label for="city">Ville</label>
    <b-form-input
      id="city"
      v-model="city"
      type="text"
      placeholder="Entrer une vile"
      name="city"
      required
    ></b-form-input>
    
    <label for="zipcode">Code postal</label>
    <b-form-input
      id="zipcode"
      v-model="zipcode"
      :state="zipcodeValidation"
      placeholder="Code postal"
      name="zipcode"
      type="text"
      required
      trim
      v-on:keyup="zipcode.length === 3 ? zipcode += '-' : zipcode"
    ></b-form-input>
    
    <input
      type="submit"
      value="Submit"
    >
  </form>
</template>

<script>
  export default {
    computed: {
      zipcodeValidation() {
        return (this.validZipcode(this.zipcode)) ? true : false;
      }
    },
    data() {
      return {
        errors: [],
        city: '',
        zipcode: '',
      }
    },
    methods: {
      checkForm: function (e) {
        this.errors = [];

        if(!this.validCity(this.city)) {
          this.errors.push('Entrer une ville valide.');
        }
        if (!this.validZipcode(this.zipcode)) {
          this.errors.push('Entrer un code postal valide.');
        }
        else
        alert('Bravo vous avez bien entrer votre ville:' + this.city + ' dont le code postal est le ' + this.zipcode)

        e.preventDefault();
      },
      validZipcode: function (zipcode) {
        var regex = /^\d{3}(?:[-]\d{4})?$/;
        return regex.test(zipcode);
      },
      validCity: function(city) {
        var regex = /[a-zA-Z0-9_]*$/;
        return regex.test(city);
      }
    }
  }
</script>
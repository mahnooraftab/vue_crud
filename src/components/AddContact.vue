<template>
  <div class="submit-form border p-4 border-info">
    <div class="form-group">
      <label for="email">Email</label>
      <input
        type="text"
        class="form-control"
        id="email"
        required
        v-model="contact.email"
        name="email"
      />
    </div>

    <div class="form-group">
      <label for="description">First name</label>
      <input
        class="form-control"
        id="first_name"
        required
        v-model="contact.first_name"
        name="first_name"
      />
    </div>

    <div class="form-group">
      <label for="last_name">Last name</label>
      <input
        class="form-control"
        id="last_name"
        required
        v-model="contact.last_name"
        name="last_name"
      />
    </div>

    <div class="form-group">
      <label for="address">Address</label>
      <input
        class="form-control"
        id="address"
        required
        v-model="contact.address"
        name="address"
      />
    </div>

    <div class="form-group">
      <label for="city">City</label>
      <input
        class="form-control"
        id="city"
        required
        v-model="contact.city"
        name="city"
      />
    </div>

    <div class="form-group">
      <label for="state">State</label>
      <input
        class="form-control"
        id="state"
        required
        v-model="contact.state"
        name="state"
      />
    </div>

    <div class="form-group">
      <label for="zipcode">Zipcode</label>
      <input
        class="form-control"
        id="zipcode"
        required
        v-model="contact.zipcode"
        name="zipcode"
      />
    </div>

    <div class="form-group">
      <label for="country">Country</label>
      <input
        class="form-control"
        id="country"
        required
        v-model="contact.country"
        name="country"
      />
    </div>

    <div class="form-group">
      <label for="phone_number">Phone number</label>
      <input
        class="form-control"
        id="phone_number"
        required
        v-model="contact.phone_number"
        name="phone_number"
      />
    </div>

    <div class="form-group">
      <label for="mail_permission">Mail permission</label>
      <input
        class="form-control"
        id="mail_permission"
        required
        v-model="contact.mail_permission"
        name="mail_permission"
      />
    </div>

    <button @click="saveContact" class="btn btn-info">Submit</button>
  </div>
  <div v-if="saved" id="message" style="display: none">
    <p>Successfully added contact</p>
  </div>
</template>

<script>
import ContactDataService from "../services/ContactDataService";

export default {
  name: "add-contact",
  data() {
    return {
      contact: {
        id: null,
        email: "",
        first_name: "",
        last_name: "",
        address: "",
        city: "",
        state: "",
        zipcode: "",
        country: "",
        phone_number: "",
        mail_permission: "",
      },
      seen: false,
    };
  },
  methods: {
    saveContact() {
      let data = {
        email: this.contact.email,
        first_name: this.contact.first_name,
        last_name: this.contact.last_name,
        address: this.contact.address,
        city: this.contact.city,
        state: this.contact.state,
        zipcode: this.contact.zipcode,
        country: this.contact.country,
        phone_number: this.contact.phone_number,
        mail_permission: this.contact.mail_permission,
      };

      ContactDataService.create(data)
        .then((response) => {
          this.contact.id = response.data.id;
          console.log(response.data);
          this.seen = true;
          this.$router.push({ name: "contacts" });
          setTimeout(function () {
            alert("Successfully saved the contact.");
          }, 1000);
        })
        .catch((e) => {
          console.log(e);
        });
    },

    newContact() {
      this.contact = {};
    },
  },
};
</script>

<style scoped>
.submit-form {
  max-width: 80%;
  text-align: left;
}
</style>

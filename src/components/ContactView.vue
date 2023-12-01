<template>
  <div
    v-if="currentContact"
    class="edit-form"
    style="max-width: 80%; text-align: left"
  >
    <form class="border p-4 border-info">
      <div class="form-group">
        <label for="email">Email</label>
        <input
          type="text"
          class="form-control"
          id="email"
          v-model="currentContact.email"
        />
      </div>
      <div class="form-group">
        <label for="first_name">First name</label>
        <input
          type="text"
          class="form-control"
          id="first_name"
          v-model="currentContact.first_name"
        />
      </div>
      <div class="form-group">
        <label for="last_name">Last name</label>
        <input
          type="text"
          class="form-control"
          id="last_name"
          v-model="currentContact.last_name"
        />
      </div>
      <div class="form-group">
        <label for="address">Address</label>
        <input
          type="text"
          class="form-control"
          id="address"
          v-model="currentContact.address"
        />
      </div>
      <div class="form-group">
        <label for="city">City</label>
        <input
          type="text"
          class="form-control"
          id="city"
          v-model="currentContact.city"
        />
      </div>
      <div class="form-group">
        <label for="state">State</label>
        <input
          type="text"
          class="form-control"
          id="state"
          v-model="currentContact.state"
        />
      </div>
      <div class="form-group">
        <label for="zipcode">Zipcode</label>
        <input
          type="text"
          class="form-control"
          id="zipcode"
          v-model="currentContact.zipcode"
        />
      </div>
      <div class="form-group">
        <label for="country">Country</label>
        <input
          type="text"
          class="form-control"
          id="country"
          v-model="currentContact.country"
        />
      </div>
      <div class="form-group">
        <label for="phone_number">Phone number</label>
        <input
          type="text"
          class="form-control"
          id="phone_number"
          v-model="currentContact.phone_number"
        />
      </div>
      <div class="form-group">
        <label for="mail_permission">Mail permission</label>
        <input
          type="text"
          class="form-control"
          id="mail_permission"
          v-model="currentContact.mail_permission"
        />
      </div>
    </form>

    <button class="btn btn-info" @click="updateContact">Update</button>
    <p>{{ message }}</p>
  </div>

  <div v-else>
    <br />
    <p>Loading</p>
  </div>
</template>

<script>
import ContactDataService from "../services/ContactDataService";

export default {
  name: "contact-view",
  data() {
    return {
      currentContact: null,
      message: "",
    };
  },
  methods: {
    getContact(id) {
      ContactDataService.get(id)
        .then((response) => {
          this.currentContact = response.data.data;
          console.log(response.data);
        })
        .catch((e) => {
          console.log(e);
        });
    },

    updateContact() {
      ContactDataService.update(this.currentContact.id, this.currentContact)
        .then((response) => {
          console.log(response.data);
          this.$router.push("/contacts");
          setTimeout(function () {
            alert("Successfully edited contact.");
          }, 1000);
        })
        .catch((e) => {
          console.log(e);
        });
    },
  },
  mounted() {
    this.message = "";
    this.getContact(this.$route.params.id);
  },
};
</script>

<style>
.edit-form {
  max-width: 300px;
  margin: auto;
}
</style>

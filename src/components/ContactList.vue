<template>
  <div class="table-responsive mt-5">
    <table class="table table bordered mt-5">
      <thead>
        <tr>
          <th>ID</th>
          <th>Email</th>
          <th>First name</th>
          <th>Last name</th>
          <th>Address</th>
          <th>City</th>
          <th>State</th>
          <th>Zipcode</th>
          <th>Country</th>
          <th>Phone number</th>
          <th>Mail permission</th>
          <th>Actions</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(contact, index) in contacts.data" :key="index">
          <td>{{ contact.id }}</td>
          <td>{{ contact.email }}</td>
          <td>{{ contact.first_name }}</td>
          <td>{{ contact.last_name }}</td>
          <td>{{ contact.address }}</td>
          <td>{{ contact.city }}</td>
          <td>{{ contact.state }}</td>
          <td>{{ contact.zipcode }}</td>
          <td>{{ contact.country }}</td>
          <td>{{ contact.phone_number }}</td>
          <td>{{ contact.mail_permission }}</td>
          <td>
            <router-link
              :to="'/contacts/' + contact?.id"
              class="badge badge-warning"
              >Edit</router-link
            >
            <br />
            <button
              class="badge badge-danger mr-2"
              @click="deleteContact(contact.id)"
            >
              Delete
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import ContactDataService from "../services/ContactDataService";

export default {
  name: "contacts-list",
  data() {
    return {
      contacts: [],
    };
  },
  methods: {
    retrieveContacts() {
      ContactDataService.getAll()
        .then((response) => {
          this.contacts = response.data;
        })
        .catch((e) => {
          console.log(e);
        });
    },
    deleteContact(id) {
      console.log(id);
      ContactDataService.delete(id)
        .then(() => {
          // this.$router.push({ name: "contacts" });
          this.retrieveContacts();
        })
        .catch((e) => {
          console.log(e);
        });
    },
  },
  mounted() {
    this.retrieveContacts();
  },
};
</script>

<style scoped>
.list {
  text-align: left;
  max-width: 750px;
  margin: auto;
}
tr {
  text-align: start;
}
</style>

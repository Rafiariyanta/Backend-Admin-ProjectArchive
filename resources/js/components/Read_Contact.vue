<template>
  <div>
    <!-- disini saya menggunakan bootstrap untuk design tabel nya. secara default bootstrap sudah di include di file welcome.blade.php jadi saya tidak perlu lagi untuk import file nya -->
    <div class="row">
      <div class="col-md-12">
        <br>
        <br>
        <div class="row">
          <div class="col-md-10">
            <h4>Contacts</h4>
          </div>
          <div class="col-md-2">
            <!-- push router ke form membuat data -->
            <router-link class="btn btn-primary w-100" to="/create">+ Tambah</router-link>
          </div>
        </div>
        <br>
        <table class="table">
          <thead>
            <tr>
              <th scope="col">Name</th>
              <th scope="col">Email</th>
              <th scope="col">Phone</th>
              <th scope="col">Message</th>
            </tr>
          </thead>
          <tbody>
            <!-- menampilkan data ke table -->
            <tr v-for="contact in contacts" :key="contact.id">
              <td style="width:20%">{{contact.name}}</td>
              <td style="width:20%">{{contact.email}}</td>
              <td style="width:20%">{{contact.phone}}</td>
              <td style="width:20%">{{contact.message}}</td>
              <td style="width:20%">
                <router-link class="btn btn-warning" :to="'/detail-contact/'+contact.id">Update</router-link>
                <button class="btn btn-danger" v-on:click="deleteData(contact.id)">Delete</button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<!-- script js -->
<script>
export default {
  data() {
    return {
      // variable array yang akan menampung hasil fetch dari api
      contacts: []
    };
  },
  created() {
    this.loadData();
  },
  methods: {
    loadData() {
      // fetch data dari api menggunakan axios
      axios.get("http://localhost:8000/api/contact").then(response => {
        // mengirim data hasil fetch ke varibale array persons
        this.contacts = response.data;
      });
    },
    deleteData(id) {
      // delete data
      axios.delete("http://localhost:8000/api/contact/" + id).then(response => {
        this.loadData();
      });
    }
  }
};
</script>
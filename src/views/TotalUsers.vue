<template>
  <div class="Users">
    <b-navbar class="is-light">
      <template #brand>
        <b-navbar-item tag="router-link" :to="{ path: '/home' }">
          <img
            src="https://etapes.com/app/uploads/2016/05/1464094938.png"
            alt="Atelier2"
          />
        </b-navbar-item>
      </template>
      <template #end>
        <b-navbar-item tag="div">
          <div>
            <b-button
              type="is-danger is-light"
              @click="deconnexion"
              class="button is-primary is-black"
              id="ButtonDeconnexion"
              >Deconnexion</b-button
            >
          </div>
        </b-navbar-item>
      </template>
      
    </b-navbar>
    <div v-for="user in users" :key="user.id" class="divusers" id="box">
          <div class="allusers">
        Prénom nom : {{ user.prenom }}
        {{ user.nom }}
        <p></p>
        Adresse email : {{ user.mail }}
          </div>
      <button
       @click="deleteUser(user.id, user.mail)"
        class="delete is-medium is-vcentered suppButton"
        id="DeleteUser"
      ></button>
      
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  name: "Users",
  components: {},
  data() {
    return {
      users: null,
      error: null,
    };
  },
  methods: {
    deconnexion() {
      this.$store.state.token = null;
      this.$router.push("/");
    },

    chargementusers() {
      axios
        .get(`http://149.91.80.75:19380/users`)
        .then((response) => (this.users = response.data));
    },

    AncienUsers() {
      this.$store.state.token = null;
      this.$router.push("/ancienusers");
    },
    deleteUser(id, label) {
      console.log("je suis la ");
      this.$buefy.dialog.confirm({
        type: "is-danger",
        cancelText: "Annuler",
        confirmText: "Accepter",
        message: `Supprimer l'utilisateur avec le mail <strong>${label}</strong> ?`,
        onConfirm: () => {
          axios
            .delete("http://149.91.80.75:19380/userSupp/" + id)
            .then((response) => {
              this.$buefy.toast.open("Utilisateur supprimée");
              axios.get("http://149.91.80.75:19380/users").then((response) => {
                this.users = response.data;
              });
            });
        },
      });
    },
  },

  created() {
    this.chargementusers();
  },
};
</script>

<style lang="scss">
.title {
  color: #48c78e;
}


.divusers{
  text-align: left;
  width: 96%;
  display: flex;
  justify-content: space-between;
  border: 2px solid rgb(206, 205, 205);
  border-radius: 5px;
  margin-left: 2%;
  margin-top:2%;
  padding-left: 5px;
  padding-top: 5px;
}

#DeleteUser{
background: red;
width: 20%;
margin-right: 5px;
margin-top: 11px;
}
</style>
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

    <div class="liste">    
    <div v-for="r in rdv" :key="r.id" id="box">
      
       Nom de l'événement : {{ r.libelle_event }}<br />
       Lieux : {{ r.libelle_lieu }}<br/>

        <button
          @click="deleteAncienRdv(r.id, r.libelle_event)"
          class="delete is-medium is-vcentered suppButton"
          id="DeleteRdv"
          
        ></button>
        
    </div> 
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
      date: null,
      rdv: null,
      error: null,
    };
  },
  methods: {
    deconnexion() {
      this.$store.state.token = null;
      this.$router.push("/");
    },

    chargementRdv() {
      axios
        .get(`http://149.91.80.75:19380/rdv`)
        .then((response) => (this.rdv = response.data));
    },
    deleteAncienRdv(id, label) {
      console.log("je suis la ");
      this.$buefy.dialog.confirm({
        type: "is-danger",
        cancelText: "Annuler",
        confirmText: "Accepter",
        message: `Supprimer le rdv avec le libelle <strong>${label}</strong> ?`,
        onConfirm: () => {
          axios
            .delete("http://149.91.80.75:19380/rdvSupp/" + id)
            .then((response) => {
              this.$buefy.toast.open("RDV supprimée");
              axios.get("http://149.91.80.75:19380/rdv").then((response) => {
                this.rdv = response.data;
              });
            });
        },
      });
    },
  },
  created() {
    this.chargementRdv();
  },
};
</script>

<style lang="scss">
#box{
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

#DeleteRdv{
background: red;
width: 20%;
margin-right: 5px;
margin-top: 11px;
}

</style>
<template>
  <div class="Bienvenue">
    <b-navbar class="is-light">
      <template #brand > 
        <b-navbar-item>
            <img
                src="https://etapes.com/app/uploads/2016/05/1464094938.png"
                alt="Atelier2"
            >
        </b-navbar-item>
      </template>
      <template #end >
        <b-navbar-item tag="div">
          <div>
            <b-button type="is-danger is-light" @click="deconnexion" class="button is-primary is-black" id="ButtonDeconnexion">Deconnexion</b-button>
          </div>
        </b-navbar-item>
      </template>
    </b-navbar>
    <div class="liste">
        <b-navbar-item class="box" id="boxusers" tag="router-link" :to="{ path: '/totalusers' } ">
          <p>Liste des Utilisateurs</p>
          <!-- <img alt="Vue logo" src="../assets/users-group.png" id="imgusers"> -->
        </b-navbar-item>
       <b-navbar-item class="box" id="boxancienusers" tag="router-link" :to="{ path: '/ancienusers' }">
          <p>Liste des Anciens Utilisateurs</p>
        </b-navbar-item>
        <b-navbar-item class="box" id="listeevents" tag="router-link" :to="{ path: '/events' }">
          <p>Liste des évents</p>
        </b-navbar-item>
        <b-navbar-item class="box" id="ancienevents" tag="router-link" :to="{ path: '/ancienevents' }">
          <p>Liste des Anciens Events</p>
        </b-navbar-item>
    </div>
    
  </div>
  
</template>
<script>


export default {
  name: "Users",
  components: {},
  data() {
    return {
      users:null,
      error: null,
    };
  },
  methods:{
    deconnexion(){
      this.$store.state.token = null;
      this.$router.push("/");
    },     
  },

  created(){
    this.chargementusers();
  },

}

</script>

<style lang="scss">

.liste{
  display: flex;
  flex-wrap: wrap;
  width: 100%;

}
#boxusers{
  margin-left: 8%;
  width: 40%;
  height: 250px;
  margin-top: 4%;
  p{
width: 100%;
  }
};
#boxancienusers{
margin-left: 5%;
 width: 40%;
height: 250px;
margin-top: 4%;
 p{
width: 100%;
  }
};
#listeevents{
  margin-left: 8%;
  width: 40%;
  height: 250px;
   p{
width: 100%;
  }
};
#ancienevents{
  margin-left: 5%;
 width: 40%;
 height: 250px;
  p{
width: 100%;
  }

};




</style>
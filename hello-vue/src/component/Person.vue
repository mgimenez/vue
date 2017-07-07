<template>
  <div class="person">
    <template v-if="person">
      <img :src="dataPerson.image" />
      <h1 v-text="dataPerson.name"></h1>
      <h2 v-text="dataPerson.email"></h2>
    </template>
    <span v-else>Cargando...</span>
  </div>
</template>

<script>
  import axios from 'axios';

  export default {
    mounted() {
      axios.get('https://randomuser.me/api/')
        .then((response) => {
          this.person = response.data.results[0];
        });
    },

    data() {
      return {
        person: null,
      }
    },

    computed: {
      dataPerson() {
        return {
          name: `${this.person.name.first} ${this.person.name.last}`,
          image: this.person.picture.large,
          email: this.person.email,
        }

      }
    }
  }
</script>

<style lang="scss">

.person {
  display: block;
  overflow: hidden;
  background-color: #c1c1c1;
  font-family: Tahoma;
  + .person {
    margin-top: 10px;
  }
  img {
    float: left;
    margin-right: 20px;
  }
}
</style>

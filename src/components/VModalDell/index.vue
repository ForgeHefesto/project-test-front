<template>
  <v-card>
    <v-card-subtitle class="pb-0">
      Você tem certeza que deseja excluir o usuario {{ date.name }} ?
    </v-card-subtitle>
    <v-card-actions>
      <v-btn color="orange" text @click="dell"> Sim </v-btn>

      <v-btn color="green" text @click="Return"> Não </v-btn>
    </v-card-actions>
  </v-card>
</template>
<script>
export default {
  props: {
    date: {
      type: Object,
      require: false,
    },
  },
  mounted() {
    console.log(this.date);
  },

  methods: {
    dell() {
      this.axios.delete(`https://project-test-back.herokuapp.com/users/${this.date._id}`).then(() =>{
        this.$emit("close");
      })
    },
    Return() {
      this.$emit("close");
    },
  },
};
</script>
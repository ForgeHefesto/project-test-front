<template>
  <v-card>
    <v-container>
      <v-card-subtitle class="pb-0 align-center" style="text-align: center">
        Você tem certeza que deseja excluir o usuario {{ date.name }} ?
      </v-card-subtitle>
      <v-card-actions>
        <v-row style="text-align: center">
          <v-col>
            <v-btn class="mr-2" depressed color="warning"  @click="dell"> Sim </v-btn>

            <v-btn depressed color="primary"  @click="Return"> Não </v-btn>
          </v-col>
        </v-row>
      </v-card-actions>
    </v-container>
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
  methods: {
    dell() {
      this.axios
        .delete(
          `https://project-test-back.herokuapp.com/users/${this.date._id}`
        )
        .then(() => {
          this.$emit("close","Usuário excluido com sucesso");
        });
    },
    Return() {
      this.$emit("return");
    },
  },
};
</script>
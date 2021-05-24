<template>
  <div>
    <v-card>
      <v-progress-linear
        v-if="loading"
        indeterminate
        color="blue darken-2"
      ></v-progress-linear>
      <v-container>
        <v-card-title>
          <span class="headline">{{ title }}</span>
        </v-card-title>
        <v-divider class="pa-3"></v-divider>

        <v-card-text>
          <v-form ref="form" v-model="valid" lazy-validation>
            <v-row>
              <v-col cols="12" sm="12" md="12">
                <v-text-field
                  v-model="date.name"
                  :counter="20"
                  :rules="nameRules"
                  label="Name"
                  required
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="12" md="12">
                <v-text-field
                  v-model="date.email"
                  :rules="emailRules"
                  label="E-mail"
                  required
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6" md="6">
                <v-text-field
                  v-model="date.cpf"
                  :rules="cpfRules"
                  type="number"
                  label="CPF"
                  :counter="11"
                  required
                ></v-text-field>
              </v-col>
              <v-col cols="12" sm="6" md="6">
                <v-text-field
                  v-model="date.phone"
                  :rules="phoneRules"
                  type="number"
                  label="Telefone"
                  :counter="11"
                  required
                ></v-text-field>
              </v-col>
              <v-divider></v-divider>
              <v-col cols="12" sm="12" md="12">
                <v-btn
                  :disabled="!valid || loading"
                  depressed
                  color="primary"
                  class="float-right"
                  @click="save(date)"
                >
                  Confirmar
                </v-btn>
              </v-col>
            </v-row>
          </v-form>
        </v-card-text>
      </v-container>
    </v-card>
  </div>
</template>
<script>
export default {
  name: "VModal",
  data: () => ({
    valid: true,
    loading: false,
    nameRules: [
      (v) => !!v || "Nome é requirido",
      (v) =>
        (v && v.length <= 20) || "Seu nome não pode ter mais que 20 letras",
    ],
    emailRules: [
      (v) => !!v || "E-mail é requirido",
      (v) => /.+@.+\..+/.test(v) || "Seu e-mail é invalido example@example.com",
    ],
    cpfRules: [
      (v) => !!v || "CPF é requirido",
      (v) => (v && v.length <= 11) || "Seu CPF não pode ter mais que 11 numeros",
    ],
    phoneRules: [
      (v) => !!v || "Telefone é requirido",
      (v) =>
        (v && v.length <= 11) || "Seu telefone não pode ter mais que 11 numeros",
    ],
  }),

  props: {
    date: {
      type: Object,
      require: false,
    },
    title: {
      type: String,
      require: true,
    },
    editModel: {
      type: Boolean,
      require: true,
    },
  },
  methods: {
    close() {
      this.$emit("close");
    },
    save(resp) {
      this.loading = true;
      if (this.editModel == true) {
        this.axios
          .put(`https://project-test-back.herokuapp.com/users/` + resp._id, resp)
          .then(() => {
            this.loading = false;
            this.$emit("save","Usuário editado com sucesso");
          })
          .catch((err) => {
            this.loading = false;
            console.log(err);
          });
      } else {
        this.axios
          .post("https://project-test-back.herokuapp.com/users", resp)
          .then(() => {
            this.loading = false;
            this.$emit("save","Usuário criado com sucesso");
          })
          .catch((err) => {
            this.loading = false;
            console.log(err);
          });
      }
    },
  },
};
</script>


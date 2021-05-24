<template>
  <v-app style="background: #ededed">
    <v-main>
      <v-dialog v-model="dialog" max-width="500px">
        <div v-if="ModelType == true">
          <VModal
            :title="title"
            :date="editedItem"
            :editModel="editModel"
            @close="close"
            @save="save"
          />
        </div>
        <div v-else>
          <VModalDell
            :date="dellUser"
            @close="close"
            @return="() => (dialog = false)"
          />
        </div>
      </v-dialog>
      <VToolbar  />
      <v-progress-linear
        v-if="loading"
        indeterminate
        color="blue darken-2"
      ></v-progress-linear>
      <v-container>
        <div class="d-flex">
          <v-row>
            <v-col cols="9">
              <h2>Lista de usuários</h2>
            </v-col>
            <v-col cols="3">
              <v-btn
                class="float-right mb-2"
                @click="newUser"
                depressed
                color="primary"
              >
                Adicionar
              </v-btn>
            </v-col>
          </v-row>
        </div>
        <VTable
          :headers="headers"
          :bodytable="bodyTable"
          @update="dialogEditModel"
          @delete="dialogDellModel"
        />
      </v-container>
      <VSnackBar :snackbar="alertModel" :text="alertText" :colorAlert="typeAlert" />
    </v-main>
  </v-app>
</template>

<script>
import VToolbar from "../../components/VToolbar/index";
import VTable from "../../components/VTable/index";
import VModal from "../../components/VModal/index";
import VModalDell from "../../components/VModalDell/index";
import VSnackBar from "../../components/VSnackBar/index";


export default {
  name: "home",

  components: {
    VToolbar,
    VTable,
    VModal,
    VModalDell,
    VSnackBar
  },
  data: () => ({
    loading: false,
    headers: [
      {
        text: "ID",
        align: "start",
        sortable: false,
        value: "_id",
      },
      { text: "Nome", value: "name" },
      { text: "Email", value: "email" },
      { text: "CPF", value: "cpf" },
      { text: "Telefone", value: "phone" },
      { text: "Ações", value: "actions", sortable: false },
    ],
    bodyTable: [],
    editedIndex: -1,
    editedItem: [],
    dellUser: [],
    dialog: false,
    editModel: false,
    ModelType: false,
    alertModel: false,
    alertText: "",
    typeAlert: "",
    title: "",
  }),

  mounted() {
    this.loading = true;
    this.init();
  },

  methods: {
    async init() {
      const raw = await this.axios.get(
        "https://project-test-back.herokuapp.com/users"
      );
      this.loading = false;
      this.bodyTable = raw.data;
    },

    UpdateStatus(res) {
      this.typeUser = res;
    },

    async dialogEditModel(id) {
      const date = await this.axios.get(
        "https://project-test-back.herokuapp.com/users/" + id
      );
      this.editedItem = date.data;
      this.title = "Ediçao de Usuário";
      this.editModel = true;
      this.dialog = true;
      this.ModelType = true;
    },

    dialogDellModel(ref) {
      this.dellUser = ref;
      this.ModelType = false;
      this.dialog = true;
    },

    newUser() {
      this.dialog = true;
      this.ModelType = true;
      (this.editedItem = {
        name: "",
        email: "",
        cpf: "",
        phone: "",
      }),
        (this.title = "Novo Usuário");
      this.editModel = false;
    },

    close(text) {
      if (text) {
        this.alertModel = true;
        this.alertText = text;
        this.typeAlert = "warning";
        this.defaultAlert();
      }
      this.dialog = false;
      this.init();
    },

    defaultAlert() {
      setTimeout(() => {
        this.alertModel = false;
      }, 9000);
    },

    save(text) {
      this.alertModel = true;
      this.alertText = text;
      this.typeAlert = "success";
      this.dialog = false;
      this.init();
    },
  },
};
</script>

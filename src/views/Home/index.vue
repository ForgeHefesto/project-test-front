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
          <VModalDell :date="dellUser" @close="close" />
        </div>
      </v-dialog>
      <VToolbar @update-Status="UpdateStatus" />
      <v-container>
        <div class="d-flex">
          <v-row>
            <v-col cols="9">
              <h2>Lista de Ativos</h2>
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
    </v-main>
  </v-app>
</template>

<script>
import VToolbar from "../../components/VToolbar/index";
import VTable from "../../components/VTable/index";
import VModal from "../../components/VModal/index";
import VModalDell from "../../components/VModalDell/index";

export default {
  name: "home",

  components: {
    VToolbar,
    VTable,
    VModal,
    VModalDell,
  },
  data: () => ({
    typeUser: null,
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
    title: "",
  }),

  mounted() {
    this.init();
  },

  methods: {
    async init() {
      const raw = await this.axios.get(
        "https://project-test-back.herokuapp.com/users"
      );
      this.bodyTable = raw.data;
    },

    UpdateStatus(res) {
      this.loading = true;
      this.typeUser = res;
    },

    async dialogEditModel(id) {
      const date = await this.axios.get(
        "https://project-test-back.herokuapp.com/users/" + id
      );
      this.editedItem = date.data;
      this.title = "Ediçao de Usuario";
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
        cpf: 0,
        phone: 0,
      }),
        (this.title = "Novo Usuario");
      this.editModel = false;
    },

    close() {
      this.dialog = false;
      this.init();
    },

    save() {
      this.dialog = false;
      this.init();
    },
  },
};
</script>

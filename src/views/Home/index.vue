<template>
  <v-app style="background: #ededed">
    <v-main>
      <v-dialog v-model="dialog" max-width="500px">
        <v-card>
          <v-container>
            <v-card-title>
              <span class="headline">{{ title }}</span>
            </v-card-title>
            <v-divider class="pa-3"></v-divider>

            <v-card-text>
              <v-row>
                <v-col cols="12" sm="12" md="12">
                  <v-text-field
                    v-model="editedItem.name"
                    label="nome"
                  ></v-text-field>
                </v-col>
                <v-col cols="12" sm="12" md="12">
                  <v-text-field
                    v-model="editedItem.email"
                    label="Email"
                  ></v-text-field>
                </v-col>
                <v-col cols="12" sm="6" md="6">
                  <v-text-field
                    v-model="editedItem.cpf"
                    label="CPF"
                  ></v-text-field>
                </v-col>
                <v-col cols="12" sm="6" md="6">
                  <v-text-field
                    v-model="editedItem.phone"
                    label="Telefone"
                  ></v-text-field>
                </v-col>
              </v-row>
            </v-card-text>
            <v-divider class="pa-3"></v-divider>
            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="close"> Cancel </v-btn>
              <v-btn color="blue darken-1" text @click="save"> Save </v-btn>
            </v-card-actions>
          </v-container>
        </v-card>
      </v-dialog>
      <VToolbar @update-Status="UpdateStatus" />
      <v-container>
        <VTable
          :headers="headers"
          :bodytable="bodyTable"
          @update="dialodEditModel"
        />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import VToolbar from "../../components/v-toolbar/index";
import VTable from "../../components/v-table/index";

export default {
  name: "App",

  components: {
    VToolbar,
    VTable,
  },
  data: () => ({
    typeUser: null,
    loading: false,
    headers: [
      {
        text: "ID",
        align: "start",
        sortable: false,
        value: "id",
      },
      { text: "Nome", value: "name" },
      { text: "Email", value: "email" },
      { text: "CPF", value: "cpf" },
      { text: "Telefone", value: "phone" },
      { text: "Actions", value: "actions", sortable: false },
    ],
    bodyTable: [
      {
        id: 1,
        name: "Matheus Santos",
        email: "matheuuss.araujo@gmail.com",
        cpf: 43085077820,
        phone: 11959834507,
      },
      {
        id: 2,
        name: "Matheus Santos",
        email: "matheuuss.araujo@gmail.com",
        cpf: 43085077820,
        phone: 11959834507,
      },
      {
        id: 3,
        name: "Matheus Santos",
        email: "matheuuss.araujo@gmail.com",
        cpf: 43085077820,
        phone: 11959834507,
      },
      {
        id: 4,
        name: "Matheus Santos",
        email: "matheuuss.araujo@gmail.com",
        cpf: 43085077820,
        phone: 11959834507,
      },
      {
        id: 5,
        name: "Matheus Santos",
        email: "matheuuss.araujo@gmail.com",
        cpf: 43085077820,
        phone: 11959834507,
      },
      {
        id: 6,
        name: "Matheus Santos",
        email: "matheuuss.araujo@gmail.com",
        cpf: 43085077820,
        phone: 11959834507,
      },
      {
        id: 7,
        name: "Matheus Santos",
        email: "matheuuss.araujo@gmail.com",
        cpf: 43085077820,
        phone: 11959834507,
      },
      {
        id: 8,
        name: "Matheus Santos",
        email: "matheuuss.araujo@gmail.com",
        cpf: 43085077820,
        phone: 11959834507,
      },
      {
        id: 9,
        name: "Matheus Santos",
        email: "matheuuss.araujo@gmail.com",
        cpf: 43085077820,
        phone: 11959834507,
      },
      {
        id: 10,
        name: "Matheus Santos",
        email: "matheuuss.araujo@gmail.com",
        cpf: 43085077819,
        phone: 11959834507,
      },
    ],
    editedIndex: -1,
    editedItem: {
      id: 0,
      name: "",
      email: "",
      cpf: 0,
      phone: 0,
    },
    dialog: false,
    title: "",
  }),

  methods: {
    UpdateStatus(res) {
      this.loading = true;
      this.typeUser = res;
    },

    dialodEditModel(ref) {
      this.title = "Ediçao de Usuario";
      console.log(ref);
      this.editedIndex = ref.indexof;
      this.editedItem = ref.date;
      this.dialog = ref.dialog;
    },

    close() {
      this.dialog = false;
    },

    save() {
      this.dialog = false;
    },
  },
};
</script>

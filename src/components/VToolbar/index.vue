<template>
  <v-card color="grey lighten-4" flat tile>
    <v-toolbar
      dense
    >
      <v-toolbar-title>Qualicorp-user</v-toolbar-title>

      <v-spacer></v-spacer>
      <v-row class="d-flex flex-row-reverse">
        <v-col cols="3">
          <v-select
            v-model="initial"
            :items="typeStyle"
            menu-props="auto"
            hide-details
            @change="handleChange(initial)"           
          />
        </v-col>
      </v-row>
    </v-toolbar>
  </v-card>
</template>
<script>
export default {
  data: () => ({
    initial: "Lista",
    typeStyle: ["Lista", "Card"],
  }),
  methods:{
      handleChange(res){
          this.$emit('update-Status', res)
      }
  }

};
</script>

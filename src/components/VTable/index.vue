<template>
  <v-data-table
    :headers="headers"
    :items="bodytable"
    :items-per-page="10"
    class="elevation-1"
  >
    <template v-slot:item.actions="{ item }">
      <v-icon color="primary" small class="mr-2" @click="editItem(item)">
        mdi-pencil
      </v-icon>
      <v-icon color="red" small @click="deleteItem(item)"> mdi-delete </v-icon>
    </template>
  </v-data-table>
</template>
<script>
export default {
  props: {
    headers: {
      type: Array,
      require: true,
    },
    bodytable: {
      type: Array,
      require: true,
    },
  },
  methods: {
     editItem(item) {
      this.$emit("update",item._id)  
    },

    deleteItem(item){
      this.$emit("delete",item)  
    }
  },
};
</script>
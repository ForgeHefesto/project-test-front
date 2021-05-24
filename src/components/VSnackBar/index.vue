<template>
  <v-snackbar center top absolute transition :color="colorAlert"  v-model="snackbar" :timeout="timeout">
    {{ text }}

    <template v-slot:action="{ attrs }">
      <v-btn :color="colorAlert" text v-bind="attrs" @click="snackbar = false">
        Close
      </v-btn>
    </template>
  </v-snackbar>
</template>

<script>
export default {
  data: () => ({
    timeout: 5000,
  }),

  props: {
    snackbar: {
      type: Boolean,
      required: false,
    },
    text: {
      type: String,
      required: false,
    },
    colorAlert: {
      type: String,
      required: false,
    },
  },
};
</script>
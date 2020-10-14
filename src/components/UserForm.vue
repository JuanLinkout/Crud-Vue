<template>
  <v-card elevation="2" class="d-flex justify-center my-12" width="600">
    <v-container fluid>
      <v-row class="d-flex justify-center">
        <v-col cols="10" md="11">
          <v-text-field
            v-model="user.fullName"
            label="Full name"
            required
          ></v-text-field>
        </v-col>
      </v-row>

      <v-row class="d-flex justify-center">
        <v-col cols="10" md="11">
          <v-text-field
            v-model="user.email"
            label="E-mail"
            required
          ></v-text-field>
        </v-col>
      </v-row>

      <v-row class="d-flex justify-center">
        <v-col cols="10" md="11">
          <v-btn color="success" class="mr-4" @click="salvar"> Send </v-btn>
          <v-btn color="error" class="mr-4" @click="resetForm">
            Reset Form
          </v-btn>
        </v-col>
      </v-row>
    </v-container>
  </v-card>
</template>

<script>
export default {
  name: "UserForm",
};
</script>
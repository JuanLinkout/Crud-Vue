<template>
  <v-app>
    <v-app-bar
      class="d-flex justify-center align-center font-weight-medium text-h3"
      app
      color="primary"
      dark
    >
      <v-toolbar-title>CRUD</v-toolbar-title>
    </v-app-bar>

    <v-main class="d-flex flex-column align-center">
      <v-card elevation="2" class="d-flex justify-center my-12" width="600">
        <v-container fluid>
          <v-row class="d-flex justify-center">
            <v-col cols="10" md="11">
              <v-text-field
                @keyup.enter="salvar(user)"
                v-model="user.fullName"
                label="Full name"
                required
              ></v-text-field>
            </v-col>
          </v-row>

          <v-row class="d-flex justify-center">
            <v-col cols="10" md="11">
              <v-text-field
                @keyup.enter="salvar(user)"
                v-model="user.email"
                label="E-mail"
                required
              ></v-text-field>
            </v-col>
          </v-row>

          <v-row class="d-flex justify-center">
            <v-col cols="10" md="11">
              <v-btn color="success" class="mr-4" @click="salvar(user)">
                Send
              </v-btn>
              <v-btn color="error" class="mr-4" @click="resetForm">
                Reset Form
              </v-btn>
            </v-col>
          </v-row>
        </v-container>
      </v-card>

      <v-card
        v-if="!animation"
        elevation="2"
        class="d-flex align-center my-12"
        width="600"
        tile
      >
        <v-list>
          <v-list-item v-for="(usuario, id) in users" :key="id" three-line>
            <v-list-item-content>
              <v-list-item-title class="my-1">
                {{ usuario.fullName }}
              </v-list-item-title>
              <v-list-item-subtitle class="my-1">
                {{ usuario.email }}
              </v-list-item-subtitle>
              <v-list-item-subtitle class="my-1">
                <v-btn
                  small
                  color="success"
                  class="mr-4"
                  @click="modify(usuario, id)"
                >
                  Change
                </v-btn>
                <v-btn small color="error" class="mr-4" @click="deleteUser(id)">
                  Delete
                </v-btn></v-list-item-subtitle
              >
            </v-list-item-content>
          </v-list-item>
        </v-list>
      </v-card>
      <v-container v-else class="d-flex justify-center align-center">
        <v-progress-circular indeterminate :size="70" color="primary" />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",

  data() {
    return {
      user: {
        fullName: "",
        email: "",
      },
      users: [],
      animation: null,
    };
  },
  methods: {
    salvar(user) {
      const method = user.id ? "put" : "post";
      const url = method === "post" ? "users.json" : `/users/${user.id}.json`;
      console.log(user);

      this.$http[method](url, this.user).then(() => {
        this.resetForm();
        this.getUsers();
      });
    },
    resetForm() {
      this.user = { fullName: "", email: "" };
    },
    deleteUser(id) {
      this.$http.delete(`/users/${id}.json`).then(() => {
        this.resetForm();
        this.getUsers();
      });
    },
    async getUsers() {
      this.animation = true;
      await this.$http.get("users.json").then((resp) => {
        this.users = { ...resp.data };
        this.animation = false;
      });
    },
    modify(user, id) {
      this.user = { ...user, id };
    },
  },
  created() {
    this.getUsers();
  },
};
</script>


<style>
.h3 {
  font-size: 1.4em;
}
</style>
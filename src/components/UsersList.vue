<template>
  <v-card elevation="2" class="d-flex align-center my-12" width="600" tile>
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
            <v-btn small color="success" class="mr-4" @click="modify">
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
</template>

<script>
export default {
  name: "UsersList",
};
</script>

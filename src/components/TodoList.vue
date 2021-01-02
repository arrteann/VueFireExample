<template>
  <div class="pt-3">
    <v-row class="d-flex justify-center">
      <v-col cols="6">
        <v-text-field
          label="New Item"
          outlined
          v-model="newItem"
          @keyup.enter="addItem"
        />
      </v-col>
      <v-col cols="1">
        <v-btn @click="addItem"> ADD </v-btn>
      </v-col>
    </v-row>
    <transition-group name="fade">
      <v-card
        class="mx-auto pa-3 ma-2 text-center"
        max-width="400"
        v-for="ToDo in ToDos"
        :key="ToDo.id"
      >
        <v-row>
          <v-col cols="8">
            <v-list-item-title class="headline mb-1">{{
              ToDo.name
            }}</v-list-item-title>
          </v-col>
          <v-col cols="4">
            <v-btn icon color="red" @click="deleteItem(ToDo.id)">
              <v-icon>mdi-delete</v-icon>
            </v-btn>
          </v-col>
        </v-row>
      </v-card>
    </transition-group>
  </div>
</template>

<script>
import { db } from "../firebase/db";
export default {
  data() {
    return {
      newItem: "",
      ToDos: [],
    };
  },
  methods: {
    addItem() {
      if (this.newItem) db.collection("ToDos").add({ name: this.newItem });
      this.newItem = "";
    },
    deleteItem(id) {
      db.collection("ToDos").doc(id).delete();
    },
  },
  firestore: {
    ToDos: db.collection("ToDos"),
  },
};
</script>

<style lang="scss" scoped>
</style>
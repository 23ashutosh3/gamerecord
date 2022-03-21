<template>
  <div>
    <v-col cols="auto" v-if="!isSignIn">
      <v-dialog transition="dialog-top-transition" max-width="600">
        <template v-slot:activator="{ on, attrs }">
          <v-btn color="primary" v-bind="attrs" v-on="on">Sign In</v-btn>
        </template>
        <template v-slot:default="dialog">
          <v-card>
            <v-toolbar color="primary" dark>Opening from the top</v-toolbar>
            <v-card-text>
              <v-form @submit.prevent="onSubmit">
                <v-text-field
                  name="UserName"
                  label="UserName"
                  type="text"
                  v-model="UserName"
                ></v-text-field>
                <v-btn type="submit" color="primary">Login</v-btn>
              </v-form>
            </v-card-text>
            <v-card-actions class="justify-end">
              <v-btn text @click="dialog.value = false">Close</v-btn>
            </v-card-actions>
          </v-card>
        </template>
      </v-dialog>
    </v-col>

    <v-col cols="auto" v-if="isSignIn">
      <template>
        <v-btn color="primary" @click="SignOutUser()">Sign Out</v-btn>
      </template>
    </v-col>
  </div>
</template>

<script>
import _ from "lodash";
export default {
  name: "Add-User",
  props: ['isSignIn'],


  data: () => ({
    LoginToggle: true,
    isEditUser: false,
    UserName: "",
    signOut: false,
  }),

  methods: {
    onSubmit() {
      if (_.isEmpty(this.UserName)) {
        return;
      } else {
        this.isEditUser = false;
        this.$emit("clicked-show-detail", this.UserName);
      }
    },
    SignOutUser() {
      this.signOut = true;
      this.$emit("changeState", this.signOut);
    },
  },
};
</script>

<style></style>

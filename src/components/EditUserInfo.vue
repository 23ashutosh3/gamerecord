<template>
  <v-dialog transition="dialog-top-transition" max-width="600">
    <template v-slot:activator="{ on, attrs }">
      <v-btn color="primary" v-bind="attrs" v-on="on">Edit User</v-btn>
    </template>
    <template v-slot:default="dialog">
      <v-card>
        <v-toolbar color="primary" dark>Edit User Details</v-toolbar>
        <v-card-text>
          <v-form @submit.prevent="onSubmitUser">
            <v-row>
              <v-col cols="12">
                <v-text-field
                  name="name"
                  label="name"
                  type="text"
                  v-model="UserData.name"
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  id="contact"
                  name="contact-number"
                  label="Contact Number"
                  type="number"
                  v-model="UserData.contact"
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  id="Age"
                  name="number"
                  label="Age"
                  type="number"
                  v-model="UserData.Age"
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  name="TotalName"
                  label="Total Match Played"
                  type="number"
                  v-model="UserData.TotalMatch"
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  id="Black"
                  name="Black"
                  label="Total match played with black"
                  type="number"
                  v-model="UserData.BlackPiece"
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  id="white"
                  name="white"
                  label="Total match played with white"
                  type="number"
                  v-model="UserData.WhitePiece"
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  label="best game move"
                  type="number"
                  required
                  v-model="UserData.BestGame"
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  id="win"
                  name="win"
                  label="Total Win"
                  type="number"
                  v-model="UserData.WinGame"
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  id="Lost"
                  name="Lost"
                  label="Total Lost"
                  type="number"
                  v-model="UserData.LostGame"
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  id="BlackWin"
                  name="BlackWin"
                  label="win with black pieces"
                  type="number"
                  v-model="UserData.BlackWin"
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  id="whiteWin"
                  name="whiteWin"
                  label="win with white pieces"
                  type="number"
                  v-model="UserData.name"
                ></v-text-field>
              </v-col>
            </v-row>
            <v-btn type="submit">Submit</v-btn>
          </v-form>
        </v-card-text>
        <v-card-actions class="justify-end">
          <v-btn text @click="dialog.value = false">Close</v-btn>
        </v-card-actions>
      </v-card>
    </template>
  </v-dialog>
</template>
<script>
export default {
  name: "EditUserInfo",
  data: () => ({
    UserData: {
      name: "",
      contact: "",
      Age: "",
      TotalMatch: "",
      BlackPiece: "",
      WhitePiece: "",
      BestGame: "",
      WinGame: "",
      LostGame: "",
      BlackWin: "",
      WhiteWin: "",
      WinPercentage: "",
    },
  }),

  methods: {
    onSubmitUser() {
      console.log("LLLLLLLLLLLLLLLLLLLLLLLLLL");
      this.$emit("updateUser", this.UserData);
    },
  },
};
</script>

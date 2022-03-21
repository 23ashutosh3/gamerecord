<template>
  <v-container>
    <h2>
      Best Game Records
    </h2>
    <v-simple-table>
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-left">first Player</th>
            <th class="text-left">Second Player</th>
            <th class="text-left">First Player Color</th>
            <th class="text-left">Second Player Color</th>
            <th class="text-left">Winner Name</th>
            <th class="text-left">Date</th>
            <th class="text-left">Best Win</th>
          </tr>
        </thead>
        <tbody>
          <tr >
            <td>{{ bestGameResult.BestGameRecord.PlayerName1 }}</td>
            <td>{{ bestGameResult.BestGameRecord.PlayerName2 }}</td>
            <td>{{ bestGameResult.BestGameRecord.Pl1Color }}</td>
            <td>{{ bestGameResult.BestGameRecord.Pl2Color }}</td>
            <td>{{ bestGameResult.BestGameRecord.Win }}</td>
            <td>{{ bestGameResult.BestGameRecord.Date }}</td>
            <td>{{ bestGameResult.BestGameRecord.BestGame }}</td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </v-container>
</template>

<script>
import async from "async";

export default {
  name: "App",
  components: {},
  props: ["User"],

  created() {
    async.parallel({
      getBestGame: () => {
        var UserData = this.User;
        UserData.sort((ele1, ele2) => {
          return ele1.BestGame - ele2.BestGame;
        });
        this.bestGameResult=UserData[0];

        console.log("<:::::<<<::<:<:<:<:<;",UserData)
      },
    });
  },

  data: () => ({
    isSignIn: true,
    LoginToggle: false,
  }),

  methods: {
    clickedShowDetailModal(SignInUser) {
      console.log(">>>>>>>>>>>>>>>>>>>>>>>>>>", SignInUser);
    },
  },
};
</script>

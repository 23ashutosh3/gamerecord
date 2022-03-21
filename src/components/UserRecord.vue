<template>
  <v-container>
    <h2>
      Top 10 Performer who played atleast 10 game from each white and black
    </h2>
    <v-simple-table>
      <template v-slot:default>
        <thead>
          <tr>
            <th class="text-left">Name</th>
            <th class="text-left">Win Game</th>

            <th class="text-left">Play with Black</th>
            <th class="text-left">Play with white</th>
            <th class="text-left">Win with white</th>
            <th class="text-left">Win with black</th>

            <th class="text-left">Lost Game</th>
            <th class="text-left">Best Game</th>
            <th class="text-left">win ratio Black vs White</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="item in populateData" :key="item.name">
            <td>{{ item.name }}</td>
            <td>{{ item.WinGame }}</td>

            <td>{{ item.BlackPiece }}</td>
            <td>{{ item.WhitePiece }}</td>
            <td>{{ item.BlackWin }}</td>
            <td>{{ item.WhiteWin }}</td>

            <td>{{ item.LostGame }}</td>
            <td>{{ item.BestGame }}</td>
            <td>{{ caculateRatio(item) }}</td>
          </tr>
        </tbody>
      </template>
    </v-simple-table>
  </v-container>
</template>

<script>
// import _ from "lodash";
import async from "async";
export default {
  name: "HelloWorld",
  props: ["User"],
  data: () => ({
    populateData: [],
  }),

  created() {
    async.parallel({
      GetTopTen: () => {
        var filtereData = this.User.filter((ele) => {
          return ele.WhitePiece >= 10 && ele.BlackPiece >= 10;
        });
        var sortData = filtereData.sort((ele1, ele2) => {
          return ele2.WinPercentage - ele1.WinPercentage;
        });
        this.populateData = sortData.slice(0, 10);
        // console.log("this.populateData", this.populateData);
      },
    });
  },

  methods: {
    caculateRatio(item) {
      var blackCol = item.BlackPiece;
      var whiteCol = item.WhitePiece;
      var blackWin = item.BlackWin;
      var whiteWin = item.WhiteWin;
      var blackWithBlackPerc = blackWin / blackCol;
      blackWithBlackPerc = Math.round(blackWithBlackPerc * 100);
      var whiteWithWhitePerc = whiteWin / whiteCol;
      whiteWithWhitePerc = Math.round(whiteWithWhitePerc * 100);
      for (var num = whiteWithWhitePerc; num > 1; num--) {
        if (blackWithBlackPerc % num == 0 && whiteWithWhitePerc % num == 0) {
          blackWithBlackPerc = blackWithBlackPerc / num;
          whiteWithWhitePerc = whiteWithWhitePerc / num;
        }
      }
      var ratio = blackWithBlackPerc + ":" + whiteWithWhitePerc;
      return ratio;
    },
  },
};
</script>

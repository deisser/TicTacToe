<template>
    <div>
        <h1>TicTacToe</h1>

        <div class="main-field" v-bind:class="{noWinner: !winner}">
            <Row v-bind:end="!winner" v-bind:input="inputValue" v-bind:lastId="lastModified" v-on:field-event="changeInput($event)"></Row>
            <Row v-bind:end="!winner" v-bind:input="inputValue" v-bind:lastId="lastModified" v-on:field-event="changeInput($event)"></Row>
            <Row v-bind:end="!winner" v-bind:input="inputValue" v-bind:lastId="lastModified" v-on:field-event="changeInput($event)"></Row>
        </div>

        <h1 v-if="winner">{{winner}} is the winner!</h1>

        <button @click="reset()">Reset</button>

    </div>
</template>

<script>
import Row from "./Row";

export default {
  name: "TicTacToe",
  components: {
    Row
  },
  data: function() {
    return {
      inputValue: "X",
      lastModified: null,
      mainField: Array.from(Array(3), () => new Array(3)),
      winner: null
    };
  },
  methods: {
    reset: function() {
      this.$children.forEach(row => {
        row.$children.forEach(field => {
          field.value = null;
        });
      });
      this.inputValue = "X";
      this.lastModified = null;
      this.mainField = Array.from(Array(3), () => new Array(3));
      this.winner = null;
    },
    changeInput: function(id) {
      this.lastModified = id;
      if (this.inputValue === "X") {
        this.inputValue = "O";
      } else {
        this.inputValue = "X";
      }
      this.checkWinner();
    },
    checkWinner: function() {
      this.$children.forEach((row, rowIndex) => {
        row.$children.forEach((field, fieldIndex) => {
          this.mainField[fieldIndex][rowIndex] = field.value;
        });
      });

      // vertical rows
      for (let index = 0; index < 3; index++) {
        var verticalRow = [];
        for (let j = 0; j < 3; j++) {
          verticalRow[j] = this.mainField[j][index];
        }
        this.findWinner(verticalRow);
      }

      // horizontal rows
      this.mainField.forEach(el => {
        this.findWinner(el);
      });

      // cross rows
      var leftCross = [
        this.mainField[0][0],
        this.mainField[1][1],
        this.mainField[2][2]
      ];
      this.findWinner(leftCross);
      var rightCross = [
        this.mainField[2][2],
        this.mainField[1][1],
        this.mainField[0][0]
      ];
      this.findWinner(rightCross);
    },
    checkArray: function(array) {
      return new Set(array).size === 1;
    },
    findWinner: function(array) {
      if (array.filter(el => el != null).length === 3) {
        if (this.checkArray(array)) {
          this.winner = array[0];
        }
      }
    }
  }
};
</script>

<style scoped>
.main-field {
  display: flex;
  justify-content: center;
}
.noWinner {
  padding-bottom: 2%;
}
</style>


<template>
  <div id="app">
    <div class="container">
      <div class="class col-10 justify-content-center mb-5">
        <h3>Token Generator</h3>
      </div>
      <div class="row justify-content-between">
        <b-form-input
          v-model="firstEmail"
          type="email"
          required
          placeholder="Enter your email address"
          class="col-9"
        ></b-form-input>
        <b-button variant="success" class="col-2" @click="emailtotoken">Convert</b-button>
        <div class="col-10 mt-2 mb-5">Token: {{ firstToken }}</div>
      </div>
      <div class="row justify-content-between">
        <b-form-input
          v-model="secondToken"
          type="text"
          required
          placeholder="Enter your token"
          class="col-9"
        ></b-form-input>
        <b-button variant="success" class="col-2" @click="tokentoemail">Convert</b-button>
        <div class="col-10 my-2">Email: {{ secondEmail }}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  components: {},
  data() {
    return {
      firstEmail: "",
      firstToken: "",
      secondEmail: "",
      secondToken: "",
      keys: ["123456789", "135792468", "147258369", "159263748", "168543297"],
      reg: /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,24}))$/
    };
  },
  methods: {
    isEmailValid() {
      return this.reg.test(this.firstEmail) ? true : false;
    },
    emailtotoken() {
      var text = this.firstEmail.toLowerCase();
      var result = "";

      if (!this.isEmailValid()) {
        this.firstToken = "inv" + result + "@pso.com";
        return;
      }

      var firstSection = text.split("@")[0];
      var secondSection = text.split("@")[1];
      var data = "";
      var domain = "";

      for (var i = 0; i < firstSection.length; i++) {
        result = this.replaceEoT(firstSection[i]) + result;
      }

      domain = secondSection.split(".");
      switch (domain[domain.length - 1]) {
        case "com":
          result = "B" + result;
          break;
        case "net":
          result = "C" + result;
          break;
        case "de":
          result = "D" + result;
          break;
        default:
          result = "A" + result;
      }

      if (result[0] === "A") {
        data = secondSection;
      } else {
        data = secondSection.substr(
          0,
          secondSection.length - domain[domain.length - 1].length - 1
        );
      }
      for (i = 0; i < data.length; i++) {
        result = this.replaceEoT(data[i]) + result;
      }

      this.firstToken = result;
    },
    tokentoemail() {
      var text = this.secondToken;
      var result = "";

      for (var i = 0; i < text.length; i++) {
        switch (text[i]) {
          case "A":
            result = "@" + result;
            break;
          case "B":
            result = "@" + result + ".com";
            break;
          case "C":
            result = "@" + result + ".net";
            break;
          case "D":
            result = "@" + result + ".de";
            break;
          default:
            result = this.replaceToE(text[i]) + result;
        }
      }
      this.secondEmail = result;
    },
    replaceEoT(letter) {
      var value = "";
      switch (letter) {
        case "0":
          value = "L";
          break;
        case "1":
          value = "M";
          break;
        case "2":
          value = "N";
          break;
        case "3":
          value = "P";
          break;
        case "4":
          value = "Q";
          break;
        case "5":
          value = "R";
          break;
        case "6":
          value = "S";
          break;
        case "7":
          value = "T";
          break;
        case "8":
          value = "U";
          break;
        case "9":
          value = "V";
          break;
        case ".":
          value = "W";
          break;
        case "-":
          value = "X";
          break;
        case "_":
          value = "Y";
          break;
        case "+":
          value = "Z";
          break;
        default:
          value = letter;
      }

      return value;
    },
    replaceToE(letter) {
      var value = "";
      switch (letter) {
        case "L":
          value = "0";
          break;
        case "M":
          value = "1";
          break;
        case "N":
          value = "2";
          break;
        case "P":
          value = "3";
          break;
        case "Q":
          value = "4";
          break;
        case "R":
          value = "5";
          break;
        case "S":
          value = "6";
          break;
        case "T":
          value = "7";
          break;
        case "U":
          value = "8";
          break;
        case "V":
          value = "9";
          break;
        case "W":
          value = ".";
          break;
        case "X":
          value = "-";
          break;
        case "Y":
          value = "_";
          break;
        case "Z":
          value = "+";
          break;
        default:
          value = letter;
      }

      return value;
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

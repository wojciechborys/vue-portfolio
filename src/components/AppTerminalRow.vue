<template>
  <section>
    <article v-for="(input, index) in inputs" :key="input.id">
      <div
        class="terminal__console--response"
        ref="console"
        v-html="input.value"
      ></div>
      <span>> :</span>
      <input
        autocomplete="off"
        v-on:keyup.enter="addInput"
        :id="input.id"
        ref="typer"
        class="terminal__console--input"
        type="text"
        @keydown.up="getPreviousCommand(index)"
        @keydown.down="getNextCommand(index)"
      />
    </article>
  </section>
</template>

<script>
export default {
  name: "AppTerminalRow",
  data() {
    return {
      counter: 0,
      inputs: [
        {
          id: 0,
          command: "",
          value: "",
        },
      ],
      commandHistory: [],
      historyIndex: -1,
    };
  },

  computed: {
    imagePath() {
      return "@/src/assets/me.jfif";
    },
  },

  methods: {
    async addInput() {
      await this.response(event.target.value);

      if (event.target.value.trim() !== "") {
        this.commandHistory.push(event.target.value);
      }

      this.$refs["typer"].forEach((input) => (input.disabled = true));
      this.$refs["typer"][this.inputs.length - 1].disabled = false;
      this.$refs["typer"][this.inputs.length - 1].focus();
    },

    response(expression) {
      let arr = [
        {
          ask: ["hi", "hello", "hey", "how are you", "welcome", "start"],
          response:
            "Welcome to my site!<br> Glad you stopped by, to learn all the commands available, just type help.",
        },
        {
          ask: ["about", "experience", "work"],
          response:
            "<img src='https://media.licdn.com/dms/image/D4D03AQGNFfl8Mo-R-Q/profile-displayphoto-shrink_800_800/0/1695977460943?e=1702512000&v=beta&t=Ph2NWqAOUbzE3SZU8kQMIgocjUEZFpUUXU7ztvz_O6s'> <br><br> My name is Wojciech Borys,<br>I'm 28 years old and I come from Olsztyn.<br>For almost 5 years, I've been working in the IT industry, primarily with WordPress.<br>Recently, I've also been developing applications based on Vue.js.<br>I've collaborated with numerous companies, both on a project basis and in ongoing B2B partnerships.<br>Most of the clients of these companies came from beyond the western border, often from Germany, the Netherlands, or the USA.<br>I run a business, and I'm not a VAT payer.",
        },

        {
          ask: ["contact", "telephone", "email"],
          response:
            "Would you like to contact me? Great! Please email me at <a href='mailto:hello@creavity.pl'>hello@creavity.pl</a>, or find me at <a target='blank' href='https://www.linkedin.com/in/wojciech-borys-261b73190/'>Linkedin</a>",
        },
        {
          ask: ["stack", "skills", "languages"],
          response:
            "I feel most comfortable with WordPress. This is probably because I've had exposure to it since the beginning of my career. I work with both WordPress and WooCommerce. <br> For some time now, I've been expanding my skills in Vue.js, and this website is a result of that. <br> In summary, I have experience in: <br> - PHP, <br> - WordPress, <br> - WooCommerce, <br> - Vue.js. <br> I use: <br> - GIT, <br> - BEM, <br> - SCSS. <br> I've created various websites and applications, ranging from simple WordPress-based projects to complex WooCommerce stores, and even a sophisticated LMS application entirely built on Vue.js.",
        },
        {
          ask: ["portfolio", "work", "projects"],
          response:
            "I will present here only a few projects, <br>- <a href='https://www.bfnky.com/' target='blank'>https://www.bfnky.com/</a><br>- <a href='https://road-cruiser.com/' target='blank'>https://road-cruiser.com/</a><br>- <a href='https://selenaesg.pl/' target='blank'>https://selenaesg.pl/</a><br>- <a href='https://mycareer.eu/' target='blank'>https://mycareer.eu/</a> <br>- <a href='https://bimasbikes.nl/' target='blank'>https://bimasbikes.nl/</a><br>- <a href='https://pijkranowke.pl/' target='blank'>https://pijkranowke.pl/</a> ",
        },
      ];

      this.inputs.push({
        id: ++this.counter,
        value: this.findResponse(expression, arr),
        command: expression,
      });
    },

    findResponse(expression, arr) {
      let response = "";
      let BreakException = {};
      let helpCommand = "help";
      let helpResponse = "List of available commands: ";

      try {
        const words = expression.toLowerCase().split(" "); // Rozdziel wyrażenie na pojedyncze słowa
        arr.forEach((value) => {
          value.ask.forEach((askPhrase) => {
            console.log(value.ask);
            if (words.some((word) => word.includes(askPhrase))) {
              response = value.response;
              throw BreakException;
            }
          });

          if (expression.toLowerCase() == helpCommand) {
            if (!response.includes(helpResponse)) {
              response = helpResponse;
            }
            response += value.ask.join(", ") + ", ";
          }
        });

        if (!response) {
          response =
            "Command not recognized, type help to get a full list of commands.";
        }
      } catch (e) {
        if (e !== BreakException) throw e;
      }

      return response;
    },

    getPreviousCommand(index) {
      if (this.historyIndex === -1) {
        this.historyIndex = this.commandHistory.length - 1;
      } else if (this.historyIndex > 0) {
        this.historyIndex--;
      }
      this.$refs["typer"][index].value = this.commandHistory[this.historyIndex];
    },

    getNextCommand(index) {
      if (this.historyIndex !== -1) {
        if (this.historyIndex < this.commandHistory.length - 1) {
          this.historyIndex++;
          this.$refs["typer"][index].value =
            this.commandHistory[this.historyIndex];
        } else {
          this.$refs["typer"][index].value = "";
          this.historyIndex = -1;
        }
      }
    },
  },
};
</script>

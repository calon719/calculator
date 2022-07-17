<script>
export default {
  data() {
    return {
      numString: '0',
      stringArr: [],
      history: '0',
      showAnswer: false,
    };
  },
  computed: {
    displayString() {
      const formattedStringArr = this.stringArr.map((string) => {
        let formattedString = '';
        if (string === '/') {
          formattedString = '÷';
        } else if (string === '*') {
          formattedString = '×';
        } else {
          formattedString = string;
        }
        return formattedString;
      });
      return formattedStringArr.join('') + this.numString;
    },
  },
  methods: {
    inputNumString(string) {
      if (this.showAnswer) {
        this.init();
      }
      if (this.numString === '0' && (string === '0' || string === '00')) {
        this.numString = '0';
      } else if (this.numString === '0' && string !== '.') {
        this.numString = string;
      } else if (string !== '.') {
        this.numString += string;
      } else if (!this.numString.includes('.') && this.numString !== '') {
        this.numString += string;
      }
    },
    setOperation(operation) {
      if (this.showAnswer) {
        this.showAnswer = false;
      }
      if (this.numString !== '') {
        this.stringArr.push(this.numString, operation);
        this.numString = '';
      }
    },
    init() {
      this.showAnswer = false;
      this.stringArr.splice(0);
      this.numString = '0';
    },
    deleteString() {
      if (this.numString === '' && this.stringArr.length !== 0) {
        this.stringArr.splice(-1, 1);
        [this.numString] = this.stringArr.splice(-1, 1);
      } else {
        this.numString = this.numString.slice(0, -1);
        if (this.numString.length <= 0) {
          this.numString = '0';
        }
      }
    },
    computeNum() {
      const answer = eval(this.stringArr.join('') + this.numString);
      this.history = `${this.displayString}<br>=${answer}`;
      this.numString = answer;
      this.stringArr.splice(0);
      this.showAnswer = true;
    },
  },
};
</script>

<template>
  <div class="rounded-lg p-8 mx-auto bg-zinc-800 w-80 drop-shadow-2xl">
    <div class="rounded-lg bg-zinc-300 px-4 py-2 mb-4">
      <div class="overflow-hidden relative">
        <p class="text-sm text-gray-500 mb-6 break-all" v-html="history" />
        <p class="text-right whitespace-nowrap absolute bottom-0 right-0">
          {{ displayString }}
        </p>
      </div>
    </div>
    <div class="grid grid-cols-4 gap-4 text-zinc-300">
      <button
        class="col-span-2 bg-red-600 py-4 text-center rounded-lg hover:opacity-70 drop-shadow-lg"
        type="button"
        @click="init"
      >
        AC
      </button>
      <button
        class="bg-red-600 py-4 text-center rounded-lg hover:opacity-70 drop-shadow-lg"
        type="button"
        @click="deleteString"
      >
        <i class="bi bi-arrow-return-left" />
      </button>
      <button
        class="bg-red-600 py-4 rounded-lg text-center w-full hover:opacity-70 drop-shadow-lg"
        type="button"
        @click="setOperation('/')"
      >
        ÷
      </button>
      <button
        class="w-full py-4 bg-purple-800 text-center rounded-lg hover:opacity-70 drop-shadow-lg"
        type="button"
        @click="inputNumString('1')"
      >
        1
      </button>
      <button
        class="w-full py-4 bg-purple-800 text-center rounded-lg hover:opacity-70 drop-shadow-lg"
        type="button"
        @click="inputNumString('2')"
      >
        2
      </button>
      <button
        class="w-full py-4 bg-purple-800 text-center rounded-lg hover:opacity-70 drop-shadow-lg"
        type="button"
        @click="inputNumString('3')"
      >
        3
      </button>
      <button
        class="bg-red-600 py-4 rounded-lg text-center w-full hover:opacity-70 drop-shadow-lg"
        type="button"
        @click="setOperation('*')"
      >
        ×
      </button>
      <button
        class="w-full py-4 bg-purple-800 text-center rounded-lg hover:opacity-70 drop-shadow-lg"
        type="button"
        @click="inputNumString('4')"
      >
        4
      </button>
      <button
        class="w-full py-4 bg-purple-800 text-center rounded-lg hover:opacity-70 drop-shadow-lg"
        type="button"
        @click="inputNumString('5')"
      >
        5
      </button>
      <button
        class="w-full py-4 bg-purple-800 text-center rounded-lg hover:opacity-70 drop-shadow-lg"
        type="button"
        @click="inputNumString('6')"
      >
        6
      </button>
      <button
        class="bg-red-600 py-4 rounded-lg text-center w-full hover:opacity-70 drop-shadow-lg"
        type="button"
        @click="setOperation('-')"
      >
        －
      </button>
      <button
        class="w-full py-4 bg-purple-800 text-center rounded-lg hover:opacity-70 drop-shadow-lg"
        type="button"
        @click="inputNumString('7')"
      >
        7
      </button>
      <button
        class="w-full py-4 bg-purple-800 text-center rounded-lg hover:opacity-70 drop-shadow-lg"
        type="button"
        @click="inputNumString('8')"
      >
        8
      </button>
      <button
        class="w-full py-4 bg-purple-800 text-center rounded-lg hover:opacity-70 drop-shadow-lg"
        type="button"
        @click="inputNumString('9')"
      >
        9
      </button>
      <button
        class="bg-red-600 py-4 rounded-lg text-center w-full hover:opacity-70 drop-shadow-lg"
        type="button"
        @click="setOperation('+')"
      >
        ＋
      </button>
      <button
        class="w-full py-4 bg-purple-800 text-center rounded-lg hover:opacity-70 drop-shadow-lg"
        type="button"
        @click="inputNumString('.')"
      >
        .
      </button>
      <button
        class="w-full py-4 bg-purple-800 text-center rounded-lg hover:opacity-70 drop-shadow-lg"
        type="button"
        @click="inputNumString('0')"
      >
        0
      </button>
      <button
        class="col-span-2 bg-amber-600 p-4 w-full text-center rounded-lg
        hover:opacity-70 drop-shadow-lg"
        type="button"
        @click="computeNum"
      >
        =
      </button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      calString: '0',
      numString: '0',
      stringArr: [],
      history: '0',
    };
  },
  watch: {
    numString() {
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
      this.calString = formattedStringArr.join('') + this.numString;
    },
  },
  methods: {
    inputNumString(string) {
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
    saveNum(operator) {
      if (this.numString !== '') {
        this.stringArr.push(this.numString, operator);
        this.numString = '';
      }
    },
    init() {
      this.stringArr.splice(0);
      this.numString = '0';
    },
  },
};
</script>

<template>
  <div class="rounded-lg p-8 mx-auto bg-zinc-800 w-80 drop-shadow-2xl">
    <div class="rounded-lg bg-zinc-300 px-4 py-2 mb-4">
      <div class="text-right overflow-hidden flex flex-col justify-end">
        <p class="text-sm text-gray-500">
          {{ history }}
        </p>
        <p>
          {{ calString }}
        </p>
      </div>
    </div>
    <div class="grid grid-cols-12 gap-4 text-zinc-300 mb-4">
      <div class="col-span-9 grid grid-cols-3 gap-4">
        <button
          v-for="num in 9"
          :key="'cal' + num"
          class="w-full py-1 bg-purple-800 text-center rounded-lg hover:opacity-70 drop-shadow-lg"
          type="button"
          @click="inputNumString(String(num))"
        >
          {{ num }}
        </button>
        <button
          class="w-full py-1 bg-purple-800 text-center rounded-lg hover:opacity-70 drop-shadow-lg"
          type="button"
          @click="inputNumString('0')"
        >
          0
        </button>
        <button
          class="w-full py-1 bg-purple-800 text-center rounded-lg hover:opacity-70 drop-shadow-lg"
          type="button"
          @click="inputNumString('00')"
        >
          00
        </button>
        <button
          class="w-full py-1 bg-purple-800 text-center rounded-lg hover:opacity-70 drop-shadow-lg"
          type="button"
          @click="inputNumString('.')"
        >
          .
        </button>
      </div>
      <div class="col-span-3">
        <button
          class="mb-4 bg-red-600 py-4 rounded-lg text-center w-full hover:opacity-70 drop-shadow-lg"
          type="button"
          @click="saveNum('/')"
        >
          ÷
        </button>
        <button
          class="mb-4 bg-red-600 py-4 rounded-lg text-center w-full hover:opacity-70 drop-shadow-lg"
          type="button"
          @click="saveNum('*')"
        >
          ×
        </button>
        <button
          class="mb-4 bg-red-600 py-4 rounded-lg text-center w-full hover:opacity-70 drop-shadow-lg"
          type="button"
          @click="saveNum('-')"
        >
          －
        </button>
        <button
          class="bg-red-600 py-4 rounded-lg text-center w-full hover:opacity-70 drop-shadow-lg"
          type="button"
          @click="saveNum('+')"
        >
          ＋
        </button>
      </div>
    </div>
    <div class="grid grid-cols-4 gap-4 text-zinc-300">
      <button
        class="bg-red-600 py-4 text-center rounded-lg hover:opacity-70 drop-shadow-lg"
        type="button"
        @click="init"
      >
        AC
      </button>
      <button
        class="bg-red-600 py-4 text-center rounded-lg hover:opacity-70 drop-shadow-lg"
        type="button"
      >
        <i class="bi bi-arrow-return-left" />
      </button>
      <button
        class="col-span-2 bg-amber-600 p-4 w-full text-center rounded-lg
        hover:opacity-70 drop-shadow-lg"
        type="button"
      >
        =
      </button>
    </div>
  </div>
</template>

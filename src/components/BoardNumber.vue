<template>
    <div :class="wMode">
        <div v-for="n in this.BoardBingo"
            class="flex flex-wrap justify-center font-semibold text-lg leading-none text-sky-400 ">
            <button v-for="Arr in n" :class="BoardNum(Arr)" @click="usersCheck()">{{ formatNumber(Arr) }}</button>
        </div>
    </div>
</template>


<script>
import CurrentNumber from './CurrentNumber.vue';

export default {
    components: {
      CurrentNumber
    },
    data() {
        return {
            Board: [
                ['B ', 'I ', 'N ', 'G ', 'O '],
                [1, 6, 11, 16, 21],
                [2, 7, 12, 17, 22],
                [3, 8, 13, 18, 23],
                [4, 9, 14, 19, 24],
                [5, 10, 15, 20, 25],
            ],
            BoardBingo: null,
        }
    },
    computed: {
        wMode() {
            let classNum = ['col-span-2 2xl:p-4 2xl:m-3 xl:p-4  m-1 mb-6 bg-sky-50 border-2 border-sky-200'];
            return classNum;
        },
        selectedNotNumber(n) {
            return this.Board[0].slice(0);
        },
        selectedNumbers() {
            return this.Board.slice(1, 6);
        },

    },
    methods: {
        formatNumber(Arr) {
            let padWidth = 0;
            let m = 25;
            for (; m >= 1; padWidth++) {
                m /= 10;
            }
            return _.padStart((Arr || 0).toString(), padWidth, '0');
        },
        BoardNum(n) {
            let classNum = ['2xl:p-5 2xl:m-3 xl:p-8 m-4 bg-sky-50 border-2 border-sky-200'];
            if (this.selectedNotNumber.includes(n)) {
                classNum.push('text-rose-800 border-rose-700');
            }
            classNum.push('');
            return classNum;
        },

    },
    mounted() {
        this.selectedNumbers
        this.BoardBingo = _.shuffle(this.Board.slice(1, 6))
        this.BoardBingo.unshift(['B ', 'I ', 'N ', 'G ', 'O '])
        this.BoardBingo[3][2] = 'ฟรี'
        console.log(this.NumberMac);
    },
}
</script>
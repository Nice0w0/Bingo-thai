<template>
        <div>
            <p class="bg-sky-500  text-center hover:bg-sky-700 text-white font-bold py-2 px-4 rounded-full">
                เลขบิงโกปัจจุบัน</p>
            <div :class="CurrentNumberC()">{{ formatNumber(currentNumber) }}
            </div>
            <div class="flex justify-center">
                <button @click="test()" v-if="!started"
                    class="bg-sky-500 hover:bg-sky-700 text-white font-bold py-2 px-4 rounded-full">
                    ประวัติออกเลขบิงโก </button>
                <button @click="reset()" v-else="started"
                    class="bg-sky-500 hover:bg-sky-700 text-white font-bold py-2 px-4 rounded-full">
                    รีเซ็ต </button>
            </div>
            <div class="flex flex-wrap justify-center mt-8 font-semibold text-lg leading-none text-sky-400 ">
                <div v-for="num in NumberMac" :class="historyNumberC(num)">
                    {{ formatNumber(num) }}
                </div>
            </div>
           
        </div>
</template>
<script>

export default
    {
        data() {
            return {
                NumberMax: [],
                NumberMac: [' B', 1, 2, 3, 4, 5, ' I', 6, 7, 8, 9, 10, ' N', 11, 12, 13, 14, 15, ' G', 16, 17, 18, 19, 20, ' O', 21, 22, 23, 24, 25],
                Numbers: 0,
                NumberCount: 0,
                NotNumber: [],
                numBingo: [],
                started: false,
                CountGame : null,
                currentNumberIndex: -1,
            }
        },
        computed: {
            currentNumber() {
                const i = this.NumberCount - 1;
                return i >= 0 && i < this.numBingo.length ? this.numBingo[i] : 0;

            },
            selectedNumbers() {
                return this.numBingo.slice(0, this.NumberCount);
            },
            selectedNotNumber() {
                let NotNum = []
                this.NotNumber = this.NumberMac
                 for(let i = 0;i<= 4; i++){
                  var p =  i * 6
                  NotNum.push(this.NotNumber[p])
                 }
                return NotNum.slice(0)
                
            },
        },
        methods: {
            formatNumber(n) {
                let padWidth = 0;
                let m = 25;
                for (; m >= 1; padWidth++) {
                   
                    m /= 10;
                }
                
                return _.padStart((n || 0).toString(), padWidth, '0');
            },
            historyNumberC(n) {
                let classNum = ['2xl:p-4 2xl:m-3 xl:p-4  m-1 mb-6 bg-sky-50 border-2 border-sky-200'];
                if (this.selectedNumbers.includes(n)) {
                    classNum.push('text-rose-800 border-rose-700');
                }
                if (this.selectedNotNumber.includes(n)) {
                    classNum.push('text-sky-900 border-sky-900');
                }
                return classNum;
            },
            test() {
                this.NumberCount++
                this.started = false
                if (this.NumberCount >= 25) {
                    this.started = true
                    clearInterval(this.CountGame)
                }
            },
            reset(){
                this.NumberCount = 0;
                this.started = false;

            },
            NumberRandom() {
              this.CountGame =  setInterval(() => {
                    // this.NumberCount++

                    //     let timerInterval
                    //     const Toast = Swal.mixin({
                    //         toast: true,
                    //         timer: 5000,
                    //         position: 'top-start',
                    //         iconColor: 'rgb(56 189 248)',
                    //         timerProgressBar: true,
                    //         showConfirmButton: false,
                    //         didOpen: () => {
                    //             timerInterval = setInterval(() => {
                    //                 Swal.getHtmlContainer().querySelector('strong').textContent = (Swal.getTimerLeft() / 1000).toFixed(0)
                    //             }, 100)


                    //         },
                    //         willClose: () => {
                    //             clearInterval(timerInterval)
                    //         }

                    //     })
                    //     Toast.fire({
                    //         icon: 'success',
                    //         html:
                    //             '<br>เกมต่อไปจะเริ่มในอีก <strong></strong> วินาที',
                    //     })
                    
                }, 5000)
            },
            CurrentNumberC() {
                let classNum = ['flex justify-center bg-sky-50 text-9xl mb-8 p-8 border-2 border-sky-200'];
                return classNum; 
            },
            NumberMaxLoop() {
                let result = [];
                for (let i = 1; i <= 25; i++) {
                    result.push(i)
                }
                this.NumberMax = result
            },
        },
        mounted() {
            this.NumberMaxLoop();
            this.NumberRandom();
            this.numBingo = _.shuffle(this.NumberMax)
            
        },
    }
</script>
<style>
* {
    font-family: 'Roboto Mono', monospace;
}
</style>
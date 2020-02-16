<template>
    <div id="calculator">
        <div class="grid-colums display-previous">
            {{ previous }} {{ process }}
        </div>
        <div class="grid-colums display-main">
            {{ display }}
        </div>
        <div class="grid-colums" @click="clearDisplay">AC</div>
        <div class="grid-colums" @click="sign">+/-</div>
        <div class="grid-colums" @click="operation('%')">%</div>
        <div class="grid-colums item2" @click="operation('/')">/</div>
        <div class="grid-colums" @click="clickNumber(7)">7</div>
        <div class="grid-colums" @click="clickNumber(8)">8</div>
        <div class="grid-colums" @click="clickNumber(9)">9</div>
        <div class="grid-colums" @click="operation('*')">X</div>
        <div class="grid-colums" @click="clickNumber(4)">4</div>
        <div class="grid-colums" @click="clickNumber(5)">5</div>
        <div class="grid-colums" @click="clickNumber(6)">6</div>
        <div class="grid-colums" @click="operation('-')">-</div>
        <div class="grid-colums" @click="clickNumber(1)">1</div>
        <div class="grid-colums" @click="clickNumber(2)">2</div>
        <div class="grid-colums" @click="clickNumber(3)">3</div>
        <div class="grid-colums" @click="operation('+')">+</div>
        <div class="grid-colums zero" @click="clickNumber(0)">0</div>
        <div class="grid-colums" @click="clickDot">.</div>
        <div class="grid-colums" @click="equal">=</div>
    </div>
</template>

<script>
export default {
    name: "MyCalender",
    data() {
        return {
            display: "0",
            previous: 0,
            process: "",
        };
    },
    methods: {
        clickDot: function() {
            if (this.display.indexOf(".") == -1) {
                this.display += ".";
                return;
            } else {
                return;
            }
        },
        clickNumber: function(e) {
            this.display += e.toString();
            this.clearZeros();
        },

        clearDisplay: function() {
            this.display = "0";
            this.previous = 0;
            this.process = "";
        },
        clearZeros: function() {
            if (this.display[1] !== ".") {
                if (this.display[0] == "0") {
                    this.display = this.display.substr(1);
                }
            }
        },
        sign: function() {
            if (this.display.indexOf("-") == 0) {
                this.display = this.display.substr(1);
            } else if (this.display.indexOf("-") == -1) {
                this.display = "-" + this.display;
            }
        },
        operation: function(e) {
            this.process = e;
            this.previous = Number(this.display);
            this.display = "0";
        },
        equal: function() {
            switch (this.process) {
                case "+":
                    this.display = String(
                        Number(this.previous) + Number(this.display),
                    );
                    break;
                case "-":
                    this.display = String(
                        Number(this.previous) - Number(this.display),
                    );
                    break;
                case "*":
                    this.display = String(
                        Number(this.previous) * Number(this.display),
                    );
                    break;
                case "/":
                    this.display = String(
                        Number(this.previous) / Number(this.display),
                    );
                    break;
                case "%":
                    this.display = String(
                        (Number(this.previous) / 100) * Number(this.display),
                    );
                    break;
                default:
                    console.log("process is empty ");
                    break;
            }
            // this.display = "0";
        },
    },
};
</script>

<style scoped>
#calculator {
    display: grid;
    grid-template-columns: repeat(4, 80px [col-start]);
    grid-template-rows: repeat(7, 80px [row-start]);
    justify-content: center;
    grid-column-gap: 10px;
    grid-row-gap: 10px;
    background-color: aquamarine;
    margin: 0 auto;
}

.grid-colums {
    border: 3px solid black;
    border-radius: 5px;
    font-size: 40px;
}
.display-previous {
    grid-column: 1/5;
    grid-row: 1;
    background-color: red;
    border: none;
    font-size: 15px;
    place-self: end;
}
.display-main {
    place-self: center stretch;
    grid-column: 1/5;
    grid-row: 2;
    background-color: blue;
}

.zero {
    grid-column: 1/3;
    grid-row: 7;
}
</style>

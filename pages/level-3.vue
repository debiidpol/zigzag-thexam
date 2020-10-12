<template>
    <div class='container level-one'>
        <div class='header'>
            <h4>LEVEL 3</h4>
            <p>Write a function that returns the minimum number of cuts needed to perform on the string such that each remaining substring is a palindrome.</p>
        </div>
        <div class='div-text'>
            <div>
                <p class='label-p'><br>Sample Input</p>
                <p>string = "noonabbad"</p>
            </div>
            <div>
                <p class='label-p'>Sample Output</p>
                <p>2 // noon | abba | d</p>
            </div>
        </div>
        <div class='div-input'>
            <div class='input-text'>
                <label for='form1'>Input String:</label>
                <div id='input-text-btn'>
                    <input type='text' id='form1' class='form-control' v-model='inputStr' onfocus='this.value=""'>
                    <button class='button' @click.stop.prevent='isPalindrome(inputStr)'>
                        <span> submit </span>
                    </button>
                </div>
            </div>
            <div class='input-text'>
                <label for='form1'>Output String:</label>
                <p v-if='isOutput'>{{output}}</p>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        data: function() {
            return {
                inputStr: '',
                output: 'no output...',
                isOutput: false
            }
        },
        methods: {
            isPalindrome(str) {
                this.isOutput = true;
                let len = str.length;

                // initialize 2d array to hold boolean values if substrings are palindrome
                let pArray = new Array(len);
                for (let i = 0; i < len; i++) {
                    pArray[i] = new Array(len);
                }

                // strings of length 1 are always palindromes
                for (let i = 0; i < len; i++) {
                    pArray[i][i] = true;
                }

                // checking if strings of length 2 are palindromes
                for (let i = 0; i < len-1; i++) {
                    if (str.charAt(i) == str.charAt(i+1)) {
                        pArray[i][i+1] = true;
                    }
                }

                //identifying if strings of length >= 3 are palindromes
                for (let i = 3; i <= len; i++) {
                    for (let j = 0; j < (len - i + 1); j++) { // traversing by length
                        let k = j+i-1;
                        if (str.charAt(j) == str.charAt(k) && pArray[j+1][k-1]) {
                            pArray[j][k] = true;
                        }
                    }
                }

                // array to hold minimum cuts for length substrings
                let pCuts = new Array(len);
                for (let i = 0; i < len; i++) {
                    let maxCut = 99999;
                    if (pArray[0][i]) {
                        pCuts[i] = 0;
                    }
                    else {
                        for (let j = 0; j < i; j++) {
                            if (pArray[j+1][i] && maxCut > pCuts[j] + 1) {
                                maxCut = pCuts[j] + 1
                            }
                        }
                        pCuts[i] = maxCut;
                    }
                }

                this.output = pCuts[len-1];
            }
        }
    }
</script>

<style>
.level-one {
  margin: 0 auto;
  min-height: 100vh;
  margin-top: 15vh;
}

.div-text {
    display: inline;
}

.label-p {
    font-weight: bold;
    margin-bottom: 0;
}

.div-input {
    display: flex;
    margin-top: 8vh;
}

.input-text {
    width: 30vw;
    margin-right: 10vw;
}

#input-text-btn {
    display: flex;
}

.button {
  border-radius: 4px;
  background-color: darkgoldenrod;
  border: none;
  color: #FFFFFF;
  text-align: center;
  /* font-size: 28px; */
  /* padding: 3vw; */
  width: 10vw;
  height: auto;
  transition: all 0.5s;
  cursor: pointer;
  margin: 5px;
  display: inline-block;
}

.button span {
  cursor: pointer;
  display: inline-block;
  position: relative;
  transition: 0.5s;
}

.button span:after {
  content: '\00bb';
  position: absolute;
  opacity: 0;
  top: 0;
  right: -20px;
  transition: 0.5s;
}

.button:hover span {
  padding-right: 25px;
}

.button:hover span:after {
  opacity: 1;
  right: 0;
}
</style>
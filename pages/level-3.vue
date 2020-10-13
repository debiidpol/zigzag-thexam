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
        <div class='div-docu'>
            <a class='docu-header' @click.stop.prevent='readMore()'>Read Technical Discussion</a>
            <div v-if='showDocu'>
                <p><br><b>Time Complexity: O(n^2)</b><br><b>Space Complexity: O(n^2)</b></p>
                <p>
                    Since a <b>palindrome</b> is a non-empty string that reads the same as backwards and forwards, characters are mirrored at the middle. <br>
                    Also, note that a string of length 1 is always a palindrome. <br><br>

                    <b>Algorithm used:</b> <br>
                    Given a string S[i..j] <br>
                    (1) we use a dynamic programming approach that: <br>
                    &emsp;&emsp;(a) takes in previously solved subproblems to a lookup (nxn) boolean array <br>
                    &emsp;&emsp;&emsp;&emsp;(i) arr[i][j] is true if S[i..j] is a palindrome <br>
                    &emsp;&emsp;&emsp;&emsp;(ii) otherwise, false <br>
                    &emsp;&emsp;(b) save the minimum number of cuts into an array of length n <br>
                    (2) traverse the whole string, and trivially, S[i..i] is a palindrome, hence arr[i][i] is true <br>
                    (3) next, we traverse and check for palindrome of strings of length 2 (S[i..i+1]) <br>
                    (4) then, we traverse again the whole string to check for palindrome of strings of length 3 or more (S[i..j]) <br>
                    &emsp;&emsp;(a) traversing the whole string starting at an index, by length 3 until n -- making substrings Sub[j..k] <br>
                    &emsp;&emsp;(b) we check if Sub[j..k] is palindrome <br>
                    &emsp;&emsp;&emsp;&emsp;(i) checking if Sub[i] === Sub[j] <br>
                    &emsp;&emsp;&emsp;&emsp;(ii) and if (i) is true, then we need to check the middle string Sub[j+1..k-1] if it is a palindrome through the lookup table at arr[j+1][k-1] <br>
                    (5) once the lookup table is all filled up from length 1..n, we update the cuts array to know the minimum number of cuts needed at the end of the string <br>
                    &emsp;&emsp;(a) traverse the whole string again and register the max integer variable <br>
                    &emsp;&emsp;(b) if from the lookup array arr[0][i] is true, it means the substring is already a palindrome, hence no need to cut and the minimum cut is 0 <br>
                    &emsp;&emsp;(c) otherwise, we traverse the whole string at Sub[j..i] <br>
                    &emsp;&emsp;&emsp;&emsp;(i) from Sub[j..i], we try to cut it and check the remaining substring Sub[j+1..i] at the right is a palindrome through the lookup table <br>
                    &emsp;&emsp;&emsp;&emsp;(ii) if Sub[j+1..i] is a palindrome, we compare the max cut to the cuts[j] + 1 and store a new max value taking the minimum cut <br>
                    &emsp;&emsp;&emsp;&emsp;(iii) we save the newest max cut at cuts[j] for Sub[j..i] <br>
                    &emsp;&emsp;(d) the value at cuts[n-1] is the minimum number of cuts that the whole string can be cut <br><br>
               
                    <b>Time and Space Complexity</b> <br>
                    The time complexity is at <b>O(n^2)</b> since every step does the traversal of the whole string runs at O(n) and for every traversal inside, it runs at O(n), too. Thus, making O(n) * O(n) = O(n^2). <br>
                    The space complexity, on the other hand, is at <b>O(n^2)</b> since we used nxn array to save the solutions to subproblems which takes up O(n^2) and a cuts array of length which takes up O(n). Thus, the algorithm uses O(n^2) + O(n) = O(n^2 + n) = O(n) space.<br><br>
                    
                </p>
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
                isOutput: false,
                showDocu: false
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
            },

            readMore() {
                this.showDocu = !this.showDocu;
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

.div-docu {
    margin-top: 10vh;
}
</style>
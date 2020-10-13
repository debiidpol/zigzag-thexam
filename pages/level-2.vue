<template>
    <div class='container level-one'>
        <div class='header'>
            <h4>LEVEL 2</h4>
            <p>Write a function that, given a string, returns its longest palindromic substring. You can assume that there will only be one longest palindromic substring.</p>
        </div>
        <div class='div-text'>
            <div>
                <p class='label-p'><br>Sample Input</p>
                <p>string = "abaxyzzyxf" </p>
            </div>
            <div>
                <p class='label-p'>Sample Output</p>
                <p>"xyzzyx"</p>
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
                <p><br><b>Time Complexity: O(n^2)</b><br><b>Space Complexity: O(1)</b></p>
                <p>
                    Since a <b>palindrome</b> is a non-empty string that reads the same as backwards and forwards, characters are mirrored at the middle. <br>
                    Also, note that a string of length 1 is always a palindrome. <br><br>

                    <b>Algorithm used:</b> <br>
                    Given a string S[i..j] <br>
                    (1) traverse the string from index 0 down to its length <br>
                    (2) at every character S[i], we run a looping method(String, int, int): <br>
                    &emsp;&emsp;(a) taking in the string S[i..j] and the current index (as center) as parameters <br>
                    &emsp;&emsp;&emsp;&emsp;(i) case 1: if the string length is odd, the method takes in i as the center <br>
                    &emsp;&emsp;&emsp;&emsp;(ii) case 2: if the string length is even, the method takes in i and i+1 as the center <br>
                    &emsp;&emsp;(b) this method compares the left and right characters of the given center if they are equal the same way as checking for palindrome <br>
                    &emsp;&emsp;(c) it loops until the left index is less than 0 and the right is greater than the string length <br>
                    &emsp;&emsp;(d) this method checks the the longest palindrome found by expanding from center to left and right and returns the length <br>
                    (3) we then find the max length between the two cases of the looping method
                    (4) with the max length, we update the starting and ending indeces of the longest palindrome found for every traversal of the given string <br><br>

                    <b>Time and Space Complexity</b> <br>
                    The time complexity is at <b>O(n^2)</b> since the traversal of the whole string runs at O(n) and for every traversal, we use the looping method which runs at O(n), too. Thus, making O(n) * O(n) = O(n^2). <br>
                    The space complexity, on the other hand, is at <b>O(1)</b> since the character comparisons and the length register of the longest palindrome only take up a constant space. <br><br>
                    
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
                isOutput: false,    // boolean to signal if the output needs to be shown already
                showDocu: false     // boolean to signal if showing the documentation part is triggered
            }
        },
        methods: {
            // function to tell whether the given string parameter is a palindrome or not
            isPalindrome(str) {
                this.isOutput = true;
                str = str.toLowerCase(); // make sure that characters are all in lower case
                str = str.replace(' ', ''); // removes whitespaces, if any
                let len = str.length;

                /*
                    Expanding from middle implementation of determining whether a non-empty string is palindrome or not.
                    > iterates through the string characters
                    > expand from left to right of the center index until valid (0...length and S[left] === S[right])
                    > save the length of the longest palindrome substring as endIndex
                    > updates new start and end index depending on the longest palindrome substring founf
                */
                if (len > 0) {
                    let startIndex = 0;
                    let endIndex = 0;

                    for (let i = 0; i < len; i++) {
                        let lengthAtOdd = this.expandAroundCenter(str, i, i);
                        let lengthAtEven = this.expandAroundCenter(str, i, i+1);
                        let longerLength = Math.max(lengthAtEven, lengthAtOdd);

                        if (longerLength > endIndex - startIndex) {
                            startIndex = i - Math.floor((longerLength-1)/2);
                            endIndex = i + Math.floor(longerLength/2)
                        }
                    }
                    this.output = str.substring(startIndex, endIndex+1)
                }
                else {
                    this.output = 'invalid input'
                }
            },

            // function that expands the palindrome substring search from left and right of the center index
            expandAroundCenter(str, center1, center2) {
                let L = center1
                let R = center2

                // validity of expansion
                while (L >= 0 && R < str.length && str.charAt(L) === str.charAt(R)) {
                    L--;
                    R++;
                }

                return R - L - 1; // returns the length of the palindrome subsrting found
            },

            // function to trigger showing the documentation div; on and off
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

.div-docu {
    margin-top: 10vh;
}
</style>
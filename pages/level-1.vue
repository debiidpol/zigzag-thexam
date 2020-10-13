<template>
    <div class='container level-one'>
        <div class='header'>
            <h4>LEVEL 1</h4>
            <p>Write a function that takes in a non-empty string and that returns a boolean representing whether the string is a palindrome.</p>
        </div>
        <div class='div-text'>
            <div>
                <p class='label-p'><br>Sample Input</p>
                <p>string = 'abcdcba'</p>
            </div>
            <div>
                <p class='label-p'>Sample Output</p>
                <p>true // it's written the same forward and backward</p>
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
                <label>Output:</label>
                <p v-if='isOutput'>{{output}}</p>
            </div>
        </div>
        <div class='div-docu'>
            <a class='docu-header' @click.stop.prevent='readMore()'>Read Technical Discussion</a>
            <div v-if='showDocu'>
                <p><br><b>Time Complexity: O(n)</b><br><b>Space Complexity: O(1)</b></p>
                <p>
                    Since a <b>palindrome</b> is a non-empty string that reads the same as backwards and forwards, characters are mirrored at the middle. <br>
                    Also, note that a string of length 1 is always a palindrome. <br><br>

                    <b>Algorithm used:</b> <br>
                    Given a string S[i..j] <br>
                    (1) traverse the string from index 0 down to its length <br>
                    (2) compare the characters from left and from right, meeting halfway (S[i] and S[j], S[i+1] and S[j-1], and so on) <br>
                    (3) a single instance of non-similar character comparison means that the string is not a palindrome <br>
                    (4) otherwise, the string is a palindrome. <br><br>

                    <b>Time and Space Complexity</b> <br>
                    The time complexity is at <b>O(n)</b> since there is technically n number of character comparisons done. <br>
                    The space complexity, on the other hand, is at <b>O(1)</b> since the character comparisons only take up a constant space.<br><br>
                    
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
                    Bruteforce implementation of determining whether a non-empty string is palindrome or not.
                    > iterates through the string characters
                    > compares end-to-end characters if equal until it reaches the middle index
                    > if all equal, then it's a plindrome; otherwise, it's not
                */
                if (len > 0 && str.match('^[a-zA-Z]*$')) {
                    let midLen = Math.floor(len / 2)
                    for (let i = 0; i < midLen; i++) {
                        if (str[i] !== str[len - i - 1]) {
                            this.output = false;
                            return;
                        }
                    }
                    this.output = true
                }
                else {;
                    this.output = 'Invalid string input'
                }
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
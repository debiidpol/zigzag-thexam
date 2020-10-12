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
                <p>Time Complexity: O(n^2)<br>Space Complexity: O(1)</p>
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
                str = str.toLowerCase();
                str = str.replace(' ', '');
                let len = str.length;

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

            expandAroundCenter(str, center1, center2) {
                let L = center1
                let R = center2

                while (L >= 0 && R < str.length && str.charAt(L) === str.charAt(R)) {
                    L--;
                    R++;
                }
                return R - L - 1;
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
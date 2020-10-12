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
        <!-- <div class='div-input'>
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
        </div> -->
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
                if (str.length > 0) {
                    let midLen = Math.floor(str.length / 2)
                    for (let i = 0; i < midLen; i++) {
                        if (str[i] !== str[str.length - i - 1]) {
                            this.output = false
                            return
                        }
                    }
                    this.output = true
                }
                else {
                    this.output = 'Invalid string'
                }
                return
            },
            doOnFocus(ins) {
                ins.value = '';
                this.isOutput = false;
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
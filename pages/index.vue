<template>
  <div class='container'>
    <b-card-group>
      <b-card
        v-for='level in levels'
        v-bind:key='level.id'
        :title='level.title'
      >
        <b-card-text> {{level.description}} </b-card-text>

        <!-- <button class='button' @click=''>
          <span>
            Run
          </span>
        </button> -->
        <nuxt-link :to='`${level.link}`'>
          <button class='button'>
            <span>
              Run
            </span>
          </button>
        </nuxt-link>
      </b-card>
    </b-card-group>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      levels: [
        {
          id: 1,
          title: 'Level 1',
          description: 'Write a function that takes in a non-empty string and that returns a boolean representing whether the string is a palindrome.',
          link: '/level-1'
        },
        {
          id: 2,
          title: 'Level 2',
          description: 'Write a function that, given a string, returns its longest palindromic substring. You can assume that there will only be one longest palindromic substring.',
          link: '/level-2'
        },
        {
          id: 3,
          title: 'Level 3',
          description: 'Write a function that returns the minimum number of cuts needed to perform on the string such that each remaining substring is a palindrome.',
          link: '/level-3'
        }
      ]
    }
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  margin-top: 25vh;
}

.card-body {
  margin: 1vw;
  text-align: left;
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

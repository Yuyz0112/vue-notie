<template>
  <div id="app">
    <div class="mask"></div>
    <main>
      <h1>Yummy Notie!</h1>
      <div class="btns">
        <a class="btn"
           v-for="(item, index) in btns"
           @click="notice(item.options)">{{ item.content }}</a>
      </div>
    </main>
    <notification
      :options.sync="options"
      :show.sync="showNotification" @close="closeNotification"></notification>
  </div>
</template>

<script>
  import Notification from './components/Notification'

  export default {
    name: 'app',
    components: {Notification},
    data () {
      return {
        showNotification: false,
        options: {},
        btns: [
          {
            content: 'success',
            options: {
              autoClose: false,
              content: 'Uhh...it tastes yummy!'
            }
          },
          {
            content: 'warning',
            options: {
              autoClose: false,
              backgroundColor: '#fbff7c',
              textColor: '#92253f',
              content: 'You can also customerize the background color and text color.'
            }
          },
          {
            content: 'error',
            options: {
              autoClose: true,
              backgroundColor: '#fc5050',
              content: 'Yummy notie can be closed automatically.'
            }
          },
          {
            content: 'info',
            options: {
              autoClose: true,
              showTime: 5000,
              backgroundColor: '#769FCD',
              content: 'There is an optional countdown bar for the auto close mode.',
              countdownBar: true,
              barColor: '#415F77'
            }
          },
          {
            content: 'flexible',
            options: {
              backgroundColor: 'rgba(6,45,146,.6)',
              content: `<P><span style="font-family: anana;font-size: 1.5rem">Yummy notie</span> is extremely flexible! You can use HTML to make any kind of notification.<br><i><a href="https://github.com/Yuyz0112/vue-notie">More information.</a></i></P>`,
              textColor: '#03D6D2'
            }
          }
        ]
      }
    },
    methods: {
      notice (options) {
        this.showNotification = true
        this.options = options
      },
      closeNotification () {
          this.showNotification = false
      }
    }
  }
</script>

<style>
  @font-face {
    font-family: anana;
    font-style: normal;
    font-weight: 400;
    src: url('./assets/anana.eot');
    src: url('./assets/anana.eot') format("eot");
    src: url('./assets/anana.woff') format("woff");
    src: url('./assets/anana.ttf') format("truetype")
  }

  * {
    margin: 0;
    padding: 0
  }

  a, a:visited {
    color: #fff
  }

  #app, .mask, body, html {
    height: 100%;
    width: 100%
  }

  #app {
    font-family: Helvetica Neue, Helvetica, Arial, Microsoft Yahei, sans-serif;
    background: url('./assets/3.jpg') 50% no-repeat;
    background-size: cover;
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column
  }

  #app .mask {
    position: absolute;
    left: 0;
    top: 0;
    background: rgba(30, 39, 68, .5)
  }

  #app main {
    position: relative;
    z-index: 2;
    width: 50%
  }

  @media screen and (max-width: 768px) {
    #app main {
      width: 100%
    }
  }

  #app main h1 {
    font-family: anana;
    font-size: 5rem;
    opacity: .75;
    color: #21e7b6;
    text-align: center
  }

  #app main .btns {
    margin-top: 3rem;
    display: flex;
    justify-content: space-around;
    width: 100%;
    margin-left: auto;
    margin-right: auto
  }

  @media screen and (max-width: 768px) {
    #app main .btns {
      flex-direction: column;
      margin-top: 1.5rem
    }
  }

  #app main .btns .btn {
    display: inline-block;
    border: 2px solid #21e7b6;
    border-radius: 5px;
    color: #fff;
    font-size: 1.5rem;
    height: 1.5rem;
    line-height: 1.5rem;
    padding: .75rem 1.5rem;
    align-items: center;
    justify-content: center;
    cursor: pointer
  }

  @media screen and (max-width: 768px) {
    #app main .btns .btn {
      width: 30%;
      margin-bottom: .5rem;
      text-align: center;
      margin-left: auto;
      margin-right: auto;
      padding: .5rem 1rem
    }
  }
</style>

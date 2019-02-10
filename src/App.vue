<template>
  <div id="app">
    <div id="devtool">
      <div class="bubble" @click="showBS = true">
        <font-awesome-icon class="icon" :icon="faCog"/>
      </div>
      <div class="overlay" :class="{ active: showBS }">
      </div>
      <div class="modal" :class="{ active: showBS }">
        <div class="modal-content">
          <font-awesome-icon class="icon close" @click="showBS = false" :icon="faTimes"/>

          <div class="item" @click="reloadPage">
            <font-awesome-icon class="icon" :icon="faSync"/>
            <span>Reload</span>
          </div>

          <div class="item" @click="openDevTools">
            <font-awesome-icon class="icon" :icon="faDev"/>
            <span>DevTools</span>
          </div>

        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { FontAwesomeIcon } from '@fortawesome/vue-fontawesome';
import { config, dom } from '@fortawesome/fontawesome-svg-core';
import {
  faSync,
  faCog,
  faTimes,
} from '@fortawesome/free-solid-svg-icons';
import { faDev } from '@fortawesome/free-brands-svg-icons';

config.autoAddCss = false;

export default {
  name: 'DevTool',
  components: {
    FontAwesomeIcon,
  },
  data() {
    return {
      showBS: false,
    };
  },
  computed: {
    faSync() {
      return faSync;
    },
    faCog() {
      return faCog;
    },
    faTimes() {
      return faTimes;
    },
    faDev() {
      return faDev;
    },
  },
  methods: {
    reloadPage() {
      const event = new Event('reloadPage');
      document.dispatchEvent(event);
    },
    openDevTools() {
      const event = new Event('openDevTools');
      document.dispatchEvent(event);
    },
  },
  mounted() {
    // This will only work on your root Vue component since it's using $parent
    const { shadowRoot } = this.$parent.$options;
    const id = 'fa-styles';

    if (!shadowRoot.getElementById(`${id}`)) {
      const faStyles = document.createElement('style');
      faStyles.setAttribute('id', id);
      faStyles.textContent = dom.css();
      shadowRoot.appendChild(faStyles);
    }
  },
};
</script>

<style>
  #devtool {
    display: flex;
    justify-content: center;

    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  .bubble {
    position: fixed;
    right: 5px;
    bottom: 5px;

    justify-content: center;

    background-color: #005fff;
    height: 50px;
    width: 50px;
    line-height: 50px;
    text-align: center;
    border-radius: 25px;
    color: #fff;
    cursor: pointer;
  }

  .overlay {
    transition: background-color .25s;
    background-color: rgba(0, 0, 0, 0.0);
    position: fixed;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
    pointer-events: none;
  }

  .overlay.active {
    background-color: rgba(0, 0, 0, 0.7);
  }

  .modal {
    transition: all .25s;
    background-color: #fff;
    position: fixed;
    bottom: -150px;
    height: 100px;
    width: 80%;

    /* material card */
    border-radius: 2px 2px 0 0;
    padding: 1rem;
  }

  .modal.active {
    bottom: 0;
    box-shadow: 0 19px 38px rgba(0, 0, 0, 0.30), 0 15px 12px rgba(0, 0, 0, 0.22);
  }

  .close {
    position: absolute;
    right: 5px;
    top: 2px;
    background-color: transparent;
    border: none;
    width: 16px;
    cursor: pointer;
    outline: none;
  }

  .modal-content {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
  }

  .item {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;

    border-radius: 2px;
    padding: 10px;
    margin: 15px;
    width: 100px;
    height: 50px;
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.12), 0 1px 2px rgba(0, 0, 0, 0.24);

    cursor: pointer;

    transition: background-color .25s;
  }

  .item:hover {
    background-color: rgba(0, 0, 0, 0.12);
  }

  .icon {
    width: 16px;
  }

  .item > .icon {
    width: 16px;
    margin: 7px;
  }
</style>

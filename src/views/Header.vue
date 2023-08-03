<template>
    <div>
      <header class="header">
        <div class="header-container">
          <div class="hamburger-icon" @click="toggleMenu">
            <img src="../assets/hamburger.png" />
          </div>
  
          <div class="header-logo-text">
            <a target="_blank" href="https://www.myllama.co/">
              <img
                class="header-logo"
                alt="Ask Llama"
                src="../assets/llama-lgo.png"
              />
            </a>
  
            <div class="header-text">
              <h1>Ask Llama</h1>
              <h2>Modern Problems. Timeless Answers</h2>
            </div>
          </div>
        </div>
      </header>
  
      <transition name="fade">
        <ul class="menu-list" v-if="showMenu">
          <!-- Back button icon -->
          <span class="back-icon" @click="toggleMenu">
            <img src="../assets/back button.png" />
          </span>
          <li>Select Masters</li>
          <li>About Us</li>
          <li>Feedback</li>
          <li>Share</li>
          <li>Privacy policy</li>
          <li>Rate Us</li>
        </ul>
      </transition>
    </div>
  </template>
  
  <script>
  export default {
    name: "AppHeader",
    data() {
      return {
        showMenu: false,
      };
    },
    methods: {
      toggleMenu() {
        this.showMenu = !this.showMenu;
      },
    },
  };
  </script>
  
  <style scoped>
  .hamburger-icon {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 30px;
    height: 30px;
    cursor: pointer;
    color: black;
    /* border: 1px solid red; */
  }
  
  .hamburger-icon > img {
    width: 100%;
    height: 100%;
  }
  .header {
    background-color: #f07812;
    color: white;
    padding: 10px;
    /* border: 1px solid red; */
  }
  
  .header-container {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    margin: 0 auto;
    /* border: 1px solid red; */
  }
  
  .header-logo-text {
    display: flex;
    align-items: center;
    flex: 1;
    justify-content: center;
    /* border: 1px solid red; */
  }
  
  .header-logo {
    width: 60px;
    height: auto;
    /* border: 1px solid red; */
  
    margin-right: 20px;
  }
  
  h1,
  h2 {
    margin: 0;
  }
  
  h1 {
    margin-bottom: 0.2rem;
    font-family: "Trebuchet MS", sans-serif;
  }
  
  h2 {
    font-size: 1.1rem;
    font-weight: 500;
    font-family: "Trebuchet MS", sans-serif;
  }
  
  .menu-list {
    /* border: 1px solid red; */
    list-style: none;
    padding: 20px;
    margin: 0;
    background-color: white;
    color: #f07812;
    position: absolute;
    top: 7px; /* Adjust the top position to your preference */
    left: 8px; /* Adjust the left position to your preference */
    z-index: 1;
    width: 150px;
    border-radius: 5px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
    font-family: sans-serif;
    text-align: left;
    cursor: pointer;
    width: 20%;
    height: 100%;
    /* border: 1px solid red; */
  }
  
  .menu-list li {
    margin-left: 1.2vw;
    padding: 20px;
    cursor: pointer;
    transition: background-color 0.2s ease;
    text-align: left;
    font-size: 25px;
  }
  
  .menu-list li:hover {
    background-color: #f07812;
    color: white;
  }
  
  .fade-enter-active,
  .fade-leave-active {
    transition: opacity 0.2s;
  }
  
  .back-icon > img {
    width: 100%;
    width: 30px;
    height: 30px;
  }
  .back-icon {
    /* border: 1px solid red; */
  }
  .fade-enter,
  .fade-leave-to {
    opacity: 0;
  }
  
  
  @media (max-width: 768px) {
    .menu-list {
      width: 89%;
      left: 0;
      top: 0;
      height: 100%;
    }
    .menu-list li {
      font-size: 20px;
    }
    .header-logo {
      display: none;
    }
  }
  </style>
  
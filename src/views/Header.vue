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
              <h2>Ask Llama</h2>
              <p>Modern Problems. Timeless Answers</p>
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
    width: 25px;
    height: 20px;
    cursor: pointer;
    color: black;
  }
  
  .hamburger-icon > img {
    width: 100%;
    height: 100%;
  }
  .header {
    background-color: #f07812;
    color: white;
    padding: 5px;
  }
  
  .header-container {
    display: flex;
    align-items: center;
    flex-wrap: wrap;
    margin: 0 auto;
  }
  
  .header-logo-text {
    display: flex;
    align-items: center;
    flex: 1;
    justify-content: center;
  }
  
  .header-logo {
    width: 50px;
    margin-right: 20px;
    margin-top: 5px;
  }
  
  h2 {
    margin-bottom: 0.2rem;
    margin: 0;
  }
  
  .menu-list {
    list-style: none;
    padding-top: 20px;
    margin: 0;
    background-color: white;
    color: #f07812;
    position: absolute;
    top: 0px; /* Adjust the top position to your preference */
    left: 0px; /* Adjust the left position to your preference */
    z-index: 1;
    border-radius: 5px;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
    cursor: pointer;
    width: 20%;
    height: 100%;
  }
  
  .menu-list li {
    margin-top: 10px;
    padding: 20px;
    cursor: pointer;
    transition: background-color 0.2s ease;
    font-size: 20px;
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

  .fade-enter,
  .fade-leave-to {
    opacity: 0;
  }

  .header-text {
    text-align: center;
  }

  .header-text p {
    color: black;
    font-size: 14px;
    font-weight: 700;
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
  
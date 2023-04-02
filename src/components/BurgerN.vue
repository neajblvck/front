<template>
    <div class="menu">
      <button class="menu-button" @click="toggleMenu">
        <span class="hamburger-icon"></span>
      </button>
      <ul class="menu-list" :class="{ 'is-active': menuIsActive }">
        <li><router-link to="/">Accueil</router-link></li>
        <li><router-link to="/about">À propos</router-link></li>
        <li><router-link to="/contact">Contact</router-link></li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    name: "BurgerNav",
    data() {
      return {
        menuIsActive: false
      }
    },
    methods: {
      toggleMenu() {
        this.menuIsActive = !this.menuIsActive;
      }
    }
  }
  </script>
  
  <style>
  .menu {
    position: relative;
  }
  
  .menu-button {
    padding: 20px 10px;
    border-radius: 8px;
    background: #00000000;
    border: none;
    cursor: pointer;
    
  }
  
  .hamburger-icon {
    display: block;
    width: 30px;
    height: 3px;
    background-color: #fff;
    position: relative;
    margin: 0 auto;
    transition: all 0.3s ease;
  }
  
  .hamburger-icon:before,
  .hamburger-icon:after {
    content: "";
    display: block;
    width: 100%;
    height: 3px;
    background-color: #fff;
    position: absolute;
    top: 0;
    left: 0;
    transition: all 0.3s ease;
  }
  
  .hamburger-icon:before {
    transform: translateY(-10px);
  }
  
  .hamburger-icon:after {
    transform: translateY(10px);
  }
  
  .menu-list {
    position: absolute;
    top: 70px;
    right: 0;
    background-color: #fff;
    width: 200px;
    padding: 20px;
    list-style: none;
    border-radius: 5px;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
    opacity: 0;
    visibility: hidden;
    transition: all 0.3s ease;
  }
  
  .menu-list.is-active {
    opacity: 1;
    visibility: visible;
    top: 100px;
  }
  </style>
  
<template>
<img id="logo" src="@/assets/icons/logo.svg">
  <label>
<input type="checkbox">
<span class="menu"> <span class="hamburger"></span><img id="logo" src="@/assets/icons/logo.svg"></span>
<ul>
  <li> <a href="#">Home</a> </li>
  <li> <a href="#">About</a> </li>
  <li> <a href="#">Contact</a> </li>
</ul>
</label>


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

#logo{
  width: 148px;
    position: fixed;
    top: 10px;
    right: 22px;
    transform: rotate(16deg);
}


label .menu {
  position: fixed;
    right: 0;
    top: 0;
    z-index: 100;
    width: 187px;
    height: 90px;
    background: #1c1c1c;
    border-radius: 0 0 0 80%;
    transition: opacity 0.3s ease;
    transition: 0.4s ease-in-out;
    box-shadow: 0 0 0 0 #000, 0 0 0 0 #000;
    cursor: pointer;
  
}

label .hamburger {
  position: absolute;
    top: 50%;
    left: 50%;
    translate: -50ù -50%;
    translate: -50%;
    width: 31px;
    height: 7px;
    background: #1c1c1c;
    display: block;
    transform-origin: center;
    transition: .5s ease-in-out;
    border-radius: 12px;
}

label .hamburger:after, label .hamburger:before {
  -webkit-transition: .5s ease-in-out;
  transition: .5s ease-in-out;
    content: "";
    position: absolute;
    display: block;
    width: 100%;
    height: 100%;
    background: #1c1c1c;
    border-radius: 12px;
}

label .hamburger:before { top: -10px; }

label .hamburger:after { bottom: -10px; }

label input { display: none; }

label input:checked + .menu {
  box-shadow: 0 0 0 100vw #FFF, 0 0 0 100vh #FFF;
  border-radius: 0;
    box-shadow: 0 0 0 128vw #1c1c1c, 0px 0px 0px 140vw white, 0px 0px 0 100vh #1c1c1c;
    border-radius: 0px 0px 0px 100%;
    border-bottom: 22px white solid;
  
}

label input:checked + .menu .hamburger {
  -webkit-transform: rotate(45deg);
  transform: rotate(45deg);
  
}

label input:checked + .menu .hamburger:after {
  -webkit-transform: rotate(90deg);
  transform: rotate(90deg);
  bottom: 0;
  
}

label input:checked + .menu .hamburger:before {
  -webkit-transform: rotate(90deg);
  transform: rotate(90deg);
  top: 0;
  
}

label input:checked + .menu + ul { opacity: 1; }

label ul {
  z-index: 200;
  position: fixed;
  top: 50%;
  left: 50%;
  -webkit-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
  opacity: 0;
  -webkit-transition: .25s 0s ease-in-out;
  transition: .25s 0s ease-in-out;
}

label a {
  margin-bottom: 1em;
  display: block;
  color: #f38630;
  text-decoration: none;
  
}

h1 {
  position: absolute;
  top: 50%;
  left: 50%;
  -webkit-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
  width: 80%;
  text-align: center;
}



  </style>
  

  
<template>
  {{ menuIsActive }}
  <!-- <label> -->
  <div class="move" ref="roundDiv" @mousedown.prevent="startDrag"
    @touchstart.prevent="startDragTouch" @touchmove.prevent="doDragTouch" @touchend="endDragTouch">

    <!-- <input @click.stop="test('input')" type="checkbox" v-model="menuIsActive"> -->
    <span class="menu" :class="{ 'shadowMenu': menuIsActive }">
      <span class="exit" :class="{ 'halbaxit': menuIsActive }"></span>
      <img class="logo" src="@/assets/icons/logo.svg" :class="{ 'halba': menuIsActive }">
    </span>
  </div>
  <!-- </label> -->


  <div @click="navigation" @wheel.prevent @touchmove.prevent @scroll.prevent :class="{ 'showNavLink': menuIsActive }"
    class="navLink">
    <ul class="ul-link">
      <li><router-link class="link" to="/">Home</router-link></li>
      <li><router-link class="link" to="/menu">LA CARTE</router-link></li>
      <li><router-link class="link" to="/admin/dashboard">Admin</router-link></li>
      <li><router-link class="link" to="/login">Login</router-link></li>
      <li><router-link class="link" to="/signup">Signup</router-link></li>
      <li><router-link class="link" to="/about">About</router-link></li>
    </ul>
  </div>
</template>
  
<script>
import { exportDefaultSpecifier } from '@babel/types'

export default {
  name: "newdeliceNav",
  data() {
    return {
      menuIsActive: false,
      isDragging: false,
      currentX: 0,
      currentY: 0,
      initialX: 0,
      initialY: 0,
      xOffset: 0,
      yOffset: 0


    }
  },

  computed: {
  },


  methods: {

    toggleMenu() {
      this.menuIsActive = !this.menuIsActive
    },

    navigation() {
      this.menuIsActive = false
    },
    startDrag(event) {  
      this.xDetectClick = event.clientX
      this.yDetectClick = event.clientY

      this.initialX = event.clientX - this.xOffset;
      this.initialY = event.clientY - this.yOffset;
      if (event.target === this.$refs.roundDiv) {
        this.isDragging = true;
        document.addEventListener("mousemove", this.doDrag);
        document.addEventListener("mouseup", this.endDrag)
      }
    },
    startDragTouch(event) {
      this.xDetectTouch = event.touches[0].clientX
      this.yDetectTouch = event.touches[0].clientY
      this.initialX = event.touches[0].clientX - this.xOffset;
      this.initialY = event.touches[0].clientY - this.yOffset;
      if (event.target === this.$refs.roundDiv) {
        this.isDragging = true;
        document.addEventListener("touchmove", this.doDragTouch)
        document.addEventListener("touchend", this.endDragTouch)
      }
    },
    doDrag(event) {
      if (this.isDragging) {
        this.currentX = event.clientX - this.initialX;
        this.currentY = event.clientY - this.initialY;
        this.xOffset = this.currentX;
        this.yOffset = this.currentY;
        this.setTranslate(this.currentX, this.currentY, this.$refs.roundDiv);
      }
    },
    doDragTouch(event) {

      if (this.isDragging) {
        this.currentX = event.touches[0].clientX - this.initialX;
        this.currentY = event.touches[0].clientY - this.initialY;
        this.xOffset = this.currentX;
        this.yOffset = this.currentY;
        this.setTranslate(this.currentX, this.currentY, this.$refs.roundDiv);
      }
    },
    endDrag(event) {
      this.isDragging = false;
      if (
        this.xDetectClick === event.clientX
        && this.yDetectClick === event.clientY
        ){this.menuIsActive = true, console.log('la')}

      this.initialX = event.clientX - this.xOffset;
      this.initialY = event.clientY - this.yOffset;
      
      document.removeEventListener("mousemove", this.doDrag);
      document.removeEventListener("mouseup", this.endDrag)



    },

    endDragTouch(event) {
      this.isDragging = false;
      if (this.xDetectTouch === event.changedTouches[0].clientX
      && this.yDetectTouch === event.changedTouches[0].clientY){
        this.menuIsActive = true
      }
      this.initialX = event.changedTouches[0].clientX;
      this.initialY = event.changedTouches[0].clientY;

      document.removeEventListener("touchmove", this.doDragTouch)
      document.removeEventListener("touchend", this.endDragTouch)


    },
    setTranslate(xPos, yPos, el) {
      el.style.transform = `translate3d(${xPos}px, ${yPos}px, 0)`;
    }
  }
}
</script>
  
<style scoped>
::-webkit-scrollbar {
  height: 0px;
  background-color: #00000000;
}


::-webkit-scrollbar-thumb {
  background-color: rgba(0, 0, 255, 0);
  height: 0;
}


::webkit-scrollbar-corner {
  background-color: rgba(0, 0, 0, 0);
  height: 0;
}

::-webkit-scrollbar-thumb:hover {
  background-color: rgba(0, 0, 0, 0);
  height: 0px;
}


.logo {
  pointer-events: none;
  width: 120%;
  position: absolute;
  top: 50%;
  translate: -49% -50%;
  left: 50%;
  transform: rotate(16deg);
  transition: 0.5s ease-in-out;
  opacity: 1;
}

.move {
  z-index: 100;
  width: 104px;
  height: 69px;
  border-radius: 28px 28px 28px 28px;
  background: #1c1c1c00;
  /* box-shadow: -1px 1px 9px 0px #0000007d, 0 0 0 0 #000; */
  position: fixed;
  transition: opacity 0.4s ease-in-out;
  margin: 30px;
  translate: 0.2 ease;
  cursor: pointer;
}




.menu {
  pointer-events: none;
  position: absolute;
  z-index: 100;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: #1C1C1C;
  border-radius: 28px 28px 28px 28px;
  transition: 0.3s ease;
  transition: 0.3s ease-in-out;
  box-shadow: -1px 1px 9px 0px #0000007d, 0 0 0 0 #000;
  cursor: pointer;
}

.shadowMenu {
  box-shadow: 0 0 0 105vw #1c1c1c00, 0 0 0 105vh #1c1c1ce0;
  border-radius: 100%;
  width: 0;
  height: 0;
  /* bottom: 50%; */
  transform: rotate(90deg);
  top: 50%;
  left: 50%;
  /* background-color: white; */
  translate: -50% -50%;

}




.exit {
  position: absolute;
  top: 50%;
  left: 50%;
  translate: -50% -50%;
  width: 31px;
  height: 7px;
  background: #ffffff;
  display: block;
  transform-origin: center;
  border-radius: 12px;
  transition: 1s cubic-bezier(0, 0.19, 0.12, 1.02);
  border-radius: 12px;
  rotate: 45deg;
  transform: scale(0.001);

}

.halbaxit {
  rotate: 2 13;
  rotate: (2turn);
  opacity: 1;
  transform: rotate(3turn);

}


.exit:after,
.exit:before {
  -webkit-transition: .5s ease-in-out;
  transition: .5s ease-in-out;
  content: "";
  position: absolute;
  display: block;
  width: 100%;
  height: 100%;
  background: #ffffff;
  border-radius: 12px;
}

.exit:before,
.exit:before {
  transform: rotate(90deg);
  top: 0;
}

.halba {
  transform: scale(0.0009) rotate(-4deg);
}






.navLink {
  visibility: hidden;
  opacity: 0;
  position: fixed;
  height: 100vh;
  width: 100vw;
  background-color: #00000005;
  z-index: 99999;
  transition: .3s 0.1s ease-in-out;
}

.showNavLink {
  visibility: visible;
  opacity: 1;
}

label input:checked+.menu+.navLink {
  opacity: 1;
}


.ul-link {
  margin: 0;
  margin-block: 0;
  padding-inline: 0;
  position: fixed;
  z-index: 9999;
  left: 50%;
  top: 40%;
  transform: translate(-50%, -50%);
  font-family: 'Subtlecurves';
  font-size: 2em;
  list-style: none;
  display: flex;
  flex-direction: column;
  align-items: center;
  transition: .3s 0.1s ease-in-out;

}


.ul-link li {
  margin-bottom: 17px;
}

.link {
  color: white;
  text-decoration: none;
  user-select: none;
}

.link:hover,
.link:hover {
  color: darkorange;
  border-bottom: 4px solid darkorange;
  padding-bottom: 8px;
}
</style>
  

  
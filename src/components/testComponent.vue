<template>
  <div class="round-div" ref="roundDiv" 
  @mousedown.stop.prevent="startDrag" 
  @mouseup.stop.prevent="endDrag"
  @touchstart.stop.prevent="startDragTouch" 
  @touchmove.stop.prevent="doDragTouch" 
  @touchend.stop.prevent="endDrag">
       </div>
</template>

<script>
import newdeliceNav from '@/components/newdeliceNav.vue';

export default {
    name: "RoundDiv",
    components: { newdeliceNav },
    data() {
        return {
            isDragging: false,
            currentX: 0,
            currentY: 0,
            initialX: 0,
            initialY: 0,
            xOffset: 0,
            yOffset: 0
        };
    },
    methods: {
        startDrag(event) {
            this.initialX = event.clientX - this.xOffset;
            this.initialY = event.clientY - this.yOffset;
            if (event.target === this.$refs.roundDiv) {
                this.isDragging = true;
                document.addEventListener("mousemove", this.doDrag);
            }
        },
        startDragTouch(event) {
            this.initialX = event.touches[0].clientX - this.xOffset;
            this.initialY = event.touches[0].clientY - this.yOffset;
            if (event.target === this.$refs.roundDiv) {
                this.isDragging = true;
            }
        },
        doDrag(event) {
            if (this.isDragging) {
                event.preventDefault();
                this.currentX = event.clientX - this.initialX;
                this.currentY = event.clientY - this.initialY;
                this.xOffset = this.currentX;
                this.yOffset = this.currentY;
                this.setTranslate(this.currentX, this.currentY, this.$refs.roundDiv);
            }
        },
        doDragTouch(event) {
            if (this.isDragging) {
                event.preventDefault();
                this.currentX = event.touches[0].clientX - this.initialX;
                this.currentY = event.touches[0].clientY - this.initialY;
                this.xOffset = this.currentX;
                this.yOffset = this.currentY;
                this.setTranslate(this.currentX, this.currentY, this.$refs.roundDiv);
            }
        },
        endDrag() {
            this.initialX = this.currentX;
            this.initialY = this.currentY;
            this.isDragging = false;
            document.removeEventListener("mousemove", this.doDrag);
        },
        setTranslate(xPos, yPos, el) {
            el.style.transform = `translate3d(${xPos}px, ${yPos}px, 0)`;
        }
    },

};
</script>

<style scoped>

</style>



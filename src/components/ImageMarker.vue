<template>
    <div class="doc-coordinates center-div" >Mark coordinates: {{ dotPosition }}</div>
    <br>
    <div class="image-container" @click="markDot($event)">
      <img :src="imageSrc" alt="Clickable image" />
      <div
        v-if="dotVisible"
        class="dot"
        :style="{ top: `${dotPosition.y}px`, left: `${dotPosition.x}px` }"
      ></div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ImageMarker',
    props: {
      imageSrc: {
        type: String,
        required: true,
      },
    },
    data() {
      return {
        dotVisible: false,
        dotPosition: { x: 0, y: 0 },
      };
    },
    methods: {
      markDot(event) {
        const rect = event.target.getBoundingClientRect();
        const x = event.clientX - rect.left; // x position within the element.
        const y = event.clientY - rect.top;  // y position within the element.
        this.dotPosition = { x, y };
        this.dotVisible = true;
      },
    },
  };
  </script>
  
  <style scoped>
  .image-container {
    position: relative;
    display: inline-block;
  }
  
  .image-container img {
    display: block; /* Removes bottom margin/whitespace */
  }
  
  .dot {
    position: absolute;
    width: 10px;
    height: 10px;
    border-radius: 50%;
    background-color: red;
    transform: translate(-50%, -50%);
  }
  .center-div {
  display: flex;
  justify-content: center;
}

  </style>
  
<template>
    <div class="d-flex justify-content-center align-items-center">
      <b-spinner
        v-for="color in colors"
        :class="color"
        :key="color"
        abel="Large Spinner"
        type="grow"
      ></b-spinner>
    </div>
</template>

<script>
export default {
  data() {
      return {
        colors: ['spinner green', 'spinner blue', 'spinner red']
      }
    }
}
</script>

<style scoped>
  .spinner {
    width: 5rem; 
    height: 5rem;    
  }

  .green {
    color: #76d376;
  }

  .blue {
    color: #8db6d8;
    animation-delay: .1s;
  }

  .red {
    color: #ff5252;
    animation-delay: .2s;
  }
</style>
<template>
    <div class="d-flex justify-content-center align-items-center">
      <b-spinner class="spinner green" label="Large Spinner" type="grow"></b-spinner>
      <b-spinner class="spinner blue" label="Large Spinner" type="grow"></b-spinner>
      <b-spinner class="spinner red" label="Large Spinner" type="grow"></b-spinner>
    </div>
</template>

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
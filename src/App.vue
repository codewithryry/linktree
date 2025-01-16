<template>
  <div>
    <!-- Loading Spinner -->
    <div v-if="isLoading" class="loading-spinner">
      <div class="spinner"></div>
      <p>Loading, please wait...</p>
    </div>

    <!-- Main Content -->
    <router-view v-else />
  </div>
</template>

<script>
export default {
  data() {
    return {
      isLoading: true, // Set to true initially to show the spinner
    };
  },
  mounted() {
    // Simulate loading delay (replace this with actual loading logic)
    setTimeout(() => {
      this.isLoading = false; // Set to false to hide the spinner
    }, 2000); // 2 seconds delay for demonstration
  },
};
</script>

<style>
/* Import the Poppins font */
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600&display=swap");

/* Loading Spinner Styles */
.loading-spinner {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background: #fefeff;
  font-family: "Poppins", sans-serif; /* Use Poppins font */
}

.spinner {
  border: 4px solid rgba(0, 0, 0, 0.1);
  border-top: 4px solid #3498db;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

.loading-spinner p {
  margin-top: 10px;
  font-size: 1rem;
  color: #333;
}
</style>
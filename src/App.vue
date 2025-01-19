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

/* Global Styles */
body {
  margin: 0;
  font-family: "Poppins", sans-serif;
  background: linear-gradient(135deg, #f4f4f9, #e0e0f0); /* Subtle gradient background */
  color: #333;
}

#app {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  padding: 20px;
  box-sizing: border-box;
}

/* Loading Spinner Styles */
.loading-spinner {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  height: 100vh; /* Full viewport height */
  text-align: center;
}

.spinner {
  border: 4px solid rgba(255, 255, 255, 0.3); /* Light border */
  border-top: 4px solid #3498db; /* Blue gradient for spinner */
  border-radius: 50%;
  width: 50px; /* Slightly larger for better visibility */
  height: 50px;
  animation: spin 1.2s cubic-bezier(0.68, -0.55, 0.27, 1.55) infinite; /* Smoother animation */
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
  margin-top: 16px; /* Increased margin for better spacing */
  font-size: 0.9rem; /* Slightly larger text */
  color: #555; /* Soft gray text color */
  font-weight: 500; /* Medium font weight */
  letter-spacing: 0.5px; /* Slight letter spacing for better readability */
}

/* Main Content Container */
.app-container {
  width: 100%;
  max-width: 800px; /* Adjust the max-width as needed */
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  overflow: hidden;
}

/* Responsive Design */
@media (max-width: 768px) {
  .spinner {
    width: 40px; /* Smaller spinner for mobile */
    height: 40px;
  }

  .loading-spinner p {
    font-size: 0.8rem; /* Smaller text for mobile */
  }
}
</style>
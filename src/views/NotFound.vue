<template>
    <div class="not-found">
      <div class="not-found-content">
        <h1>404</h1>
        <h2>Page Not Found</h2>
        <p>Oops! The page you're looking for doesn't exist or has been moved.</p>
        <router-link to="/" class="home-link">Go back to the home page</router-link>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'NotFound'
  }
  </script>
  
  <style scoped>
  .not-found {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    color: #fff;
    font-family: 'Poppins', sans-serif;
    text-align: center;
    margin-top: -100px;
  }
  
  .not-found-content {
    background: rgba(255, 255, 255, 0.1);
    padding: 40px;
    border-radius: 15px;
    animation: fadeIn 1s ease-in-out;
  }
  
  h1 {
    font-size: 6rem;
    margin: 0;
    font-weight: 700;
    color: #000000;
    text-shadow: 2px 2px 4px rgba(255, 255, 255, 0.3);
  }
  
  h2 {
    font-size: 2rem;
    margin: 10px 0;
    font-weight: 600;
    color: #000000;
    text-shadow: 1px 1px 2px rgba(255, 255, 255, 0.2);
  }
  
  p {
    font-size: 1.2rem;
    margin: 20px 0;
    color: #000000;
  }
  
  .home-link {
    display: inline-block;
    margin-top: 20px;
    padding: 12px 24px;
    font-size: 1rem;
    font-weight: 500;
    color: #ffffff;
    background: #000000;
    border-radius: 30px;
    text-decoration: none;
    transition: all 0.3s ease;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }
  
  .home-link:hover {

    transform: translateY(-2px);
    box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
  }
  
  @keyframes fadeIn {
    from {
      opacity: 0;
      transform: translateY(-20px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }
  </style>
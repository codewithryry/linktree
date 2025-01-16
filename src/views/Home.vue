<template>
  <div class="linktree-container">
    <div class="linktree">
      <!-- Profile Section -->
      <div class="profile">
        <img :src="profile.image" alt="Profile Picture" class="profile-image" />
        <h1>{{ profile.name }}</h1>
        <p class="bio">{{ profile.bio }}</p>
        <p class="username">@{{ profile.username }} on tiktok</p>
      </div>

      <!-- Search Bar -->
      <div class="search-bar">
        <input
          type="text"
          v-model="searchQuery"
          placeholder="Search links..."
          class="search-input"
        />
        <i class="fas fa-search search-icon"></i>
      </div>
      <br />

      <!-- Links Section -->
      <div class="links">
        <!-- Dropdown for GitHub Links -->
        <div class="dropdown">
          <button
            class="link-button dropdown-toggle"
            @click="toggleDropdown('github')"
            :aria-expanded="isDropdownOpen.github"
          >
            <i class="fab fa-github icon"></i>
            <span>GitHub Projects</span>
            <i
              class="fas fa-chevron-down dropdown-icon"
              :class="{ rotate: isDropdownOpen.github }"
            ></i>
          </button>
          <transition name="slide">
            <div
              class="dropdown-content"
              v-if="isDropdownOpen.github"
              aria-label="GitHub Projects Dropdown"
            >
              <a
                v-for="link in filteredGithubLinks"
                :key="link.id"
                :href="link.url"
                target="_blank"
                rel="noopener noreferrer"
                class="dropdown-link"
              >
                <i :class="link.icon" class="icon"></i>
                <span>{{ link.label }}</span>
              </a>
            </div>
          </transition>
        </div>

        <!-- Dropdown for Social Media Links -->
        <div class="dropdown">
          <button
            class="link-button dropdown-toggle"
            @click="toggleDropdown('social')"
            :aria-expanded="isDropdownOpen.social"
          >
            <i class="fas fa-share-alt icon"></i>
            <span>Social Media</span>
            <i
              class="fas fa-chevron-down dropdown-icon"
              :class="{ rotate: isDropdownOpen.social }"
            ></i>
          </button>
          <transition name="slide">
            <div
              class="dropdown-content"
              v-if="isDropdownOpen.social"
              aria-label="Social Media Dropdown"
            >
              <a
                v-for="link in filteredSocialLinks"
                :key="link.id"
                :href="link.url"
                target="_blank"
                rel="noopener noreferrer"
                class="dropdown-link"
                :class="{ disabled: link.url === '#' }"
                @click="handleLinkClick(link.url)"
              >
                <i :class="link.icon" class="icon"></i>
                <span>{{ link.label }}</span>
              </a>
            </div>
          </transition>
        </div>

        <!-- Other Links -->
        <a
          v-for="link in filteredOtherLinks"
          :key="link.id"
          :href="link.url"
          target="_blank"
          rel="noopener noreferrer"
          class="link-button"
          :download="link.label === 'Resume' ? 'Resume.pdf' : null"
        >
          <i :class="link.icon" class="icon"></i>
          <span>{{ link.label }}</span>
        </a>
      </div>

      <!-- Footer Section -->
      <footer class="footer">
        <p class="footer-text">Developed by codewithryry.</p>
      </footer>
    </div>

    <!-- Back-to-Top Button -->
    <button
      v-if="showBackToTop"
      @click="scrollToTop"
      class="back-to-top"
      aria-label="Back to Top"
    >
      <i class="fas fa-arrow-up"></i>
    </button>
  </div>
</template>

<script>
export default {
  name: "LinktreeView",
  data() {
    return {
      isDropdownOpen: {
        github: false,
        social: false,
      },
      profile: {
        name: "Reymel Mislang",
        bio: "Transforming ideas into interactive experiences, one line of code at a time.",
        username: "betsyoneontg",
        image: require("@/assets/profile.jpg"),
      },
      links: [
        {
          id: 1,
          label: "GitHub Profile",
          url: "https://github.com/codewithryry",
          icon: "fab fa-github",
        },
        {
          id: 2,
          label: "BoyloveYSeriesHub",
          url: "https://boyloveyserieshub.vercel.app/",
          icon: "fas fa-film",
        },
        {
          id: 3,
          label: "SafePath",
          url: "https://safepath-4pzk.onrender.com/",
          icon: "fas fa-shield-alt",
        },
        {
          id: 4,
          label: "SafePath Prototype",
          url: "https://github.com/codewithryry/minsu-safepath",
          icon: "fas fa-code-branch",
        },
        {
          id: 5,
          label: "Trabahanap Job Analyzer",
          url: "https://github.com/codewithryry/Trabahanap-job-matching-analyzer",
          icon: "fas fa-briefcase",
        },
        {
          id: 6,
          label: "Portfolio",
          url: "https://reymel-mislang.onrender.com/",
          icon: "fas fa-user",
        },
        {
          id: 7,
          label: "WakaTime",
          url: "https://wakatime.com/@codewithryry",
          icon: "fas fa-chart-line",
        },
        {
          id: 13,
          label: "Resume",
          url: "/Resume.pdf",
          icon: "fas fa-file-pdf",
        },
        {
          id: 14,
          label: "Email",
          url: "mailto:reymelrey.mislang@gmail.com",
          icon: "fas fa-envelope",
        },
      ],
      socialLinks: [
        {
          id: 5,
          label: "Spotify",
          icon: "fab fa-spotify",
          url: "https://open.spotify.com/user/yzay8x8u0lqinlp7mbxuy24aj",
        },
        {
          id: 2,
          label: "Twitter",
          icon: "fab fa-twitter",
          url: "#",
        },
        {
          id: 3,
          label: "Instagram",
          icon: "fab fa-instagram",
          url: "#",
        },
        {
          id: 4,
          label: "YouTube",
          icon: "fab fa-youtube",
          url: "#",
        },
      ],
      searchQuery: "",
      showBackToTop: false,
    };
  },
  computed: {
    githubLinks() {
      return this.links.filter(
        (link) =>
          link.icon.includes("github") ||
          link.icon.includes("code-branch") ||
          link.label === "BoyloveYSeriesHub" ||
          link.label === "SafePath" ||
          link.label === "SafePath Prototype" ||
          link.label === "Trabahanap Job Analyzer"
      );
    },
    otherLinks() {
      return this.links.filter((link) => !this.githubLinks.includes(link));
    },
    filteredGithubLinks() {
      return this.githubLinks.filter((link) =>
        link.label.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
    filteredSocialLinks() {
      return this.socialLinks.filter((link) =>
        link.label.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
    filteredOtherLinks() {
      return this.otherLinks.filter((link) =>
        link.label.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
  },
  methods: {
    toggleDropdown(type) {
      this.isDropdownOpen[type] = !this.isDropdownOpen[type];
    },
    handleLinkClick(url) {
      if (url === "#") {
        alert("This link is not available yet.");
        event.preventDefault();
      }
    },
    handleScroll() {
      this.showBackToTop = window.scrollY > 200;
    },
    scrollToTop() {
      window.scrollTo({ top: 0, behavior: "smooth" });
    },
  },
  mounted() {
    window.addEventListener("scroll", this.handleScroll);
  },
  beforeDestroy() {
    window.removeEventListener("scroll", this.handleScroll);
  },
};
</script>

<style scoped>
/* Global Styles */
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600&display=swap");

.linktree-container {
  position: relative;
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
}

.linktree {
  font-family: "Poppins", sans-serif;
  margin: 0;
  padding: 20px;
  color: #000;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}

/* Profile Section */
.profile {
  margin-bottom: 40px;
}

.profile-image {
  width: 120px;
  height: 120px;
  border-radius: 50%;
  margin-bottom: 15px;
  border: 4px solid #000;
  box-shadow: 0 4px 20px rgba(255, 255, 255, 0.1);
}

.profile h1 {
  font-size: 2rem;
  margin: 10px 0 5px;
  color: #000;
  font-weight: 600;
}

.bio {
  font-size: 1rem;
  color: #333;
  margin-top: 5px;
  line-height: 1.5;
  font-weight: 400;
}

.username {
  font-size: 0.9rem;
  color: #666;
  margin-top: 5px;
  font-weight: 500;
}

/* Search Bar */
.search-bar {
  width: 100%;
  max-width: 500px;
  margin-bottom: 20px;
  position: relative;
}

.search-input {
  width: 87%;
  padding: 12px 40px 12px 16px;
  border: 2px solid #000;
  border-radius: 25px;
  font-size: 1rem;
  outline: none;
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
  background: #fff;
  color: #000;
}

.search-input:focus {
  border-color: #000;
  box-shadow: 0 0 8px rgba(0, 0, 0, 0.3);
}

.search-icon {
  position: absolute;
  right: 16px;
  top: 50%;
  transform: translateY(-50%);
  color: #000;
  font-size: 1.2rem;
  pointer-events: none;
}

/* Links Section */
.links {
  width: 100%;
  max-width: 500px;
  display: flex;
  flex-direction: column;
  gap: 15px;
  padding: 0 20px;
}

.link-button {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  padding: 15px;
  color: #000;
  text-align: left;
  text-decoration: none;
  border-radius: 12px;
  font-size: 1rem;
  transition: transform 0.3s ease, box-shadow 0.3s ease, opacity 0.2s ease;
  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.1);
  background: #fff;
  border: 1px solid #000;
}

.link-button:hover {
  transform: translateY(-3px);
  box-shadow: 0 6px 15px rgba(0, 0, 0, 0.2);
  opacity: 0.9;
}

.icon {
  margin-right: 10px;
  font-size: 1.2rem;
  color: #000;
}

/* Dropdown Styles */
.dropdown {
  position: relative;
}

/* Dropdown Toggle Button */
.dropdown-toggle {
  width: 100%;
  cursor: pointer;
  font-size: 1rem;
  color: #000;
  font-family: 'Poppins', sans-serif; /* Add Poppins font */
  display: flex;
  align-items: center;
  justify-content: flex-start;
  padding: 15px;
  text-align: left;
  text-decoration: none;
  border-radius: 12px;
  transition: transform 0.3s ease, box-shadow 0.3s ease, opacity 0.2s ease;
  box-shadow: 0 3px 6px rgba(0, 0, 0, 0.1);
  background: #fff;
  border: 1px solid #000;
}

/* Ensure the <span> inside the dropdown toggle uses Poppins */
.dropdown-toggle span {
  font-size: 1rem;
  color: #000;
  font-family: 'Poppins', sans-serif; /* Add Poppins font */
}


.dropdown-icon {
  margin-left: auto;
  transition: transform 0.3s ease;
  color: #000;
}

.dropdown-icon.rotate {
  transform: rotate(180deg);
}

.dropdown-content {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-top: 10px;
  background: #fff;
  border-radius: 12px;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
  padding: 10px;
  border: 1px solid #000;
}

.dropdown-link {
  display: flex;
  align-items: center;
  padding: 10px;
  color: #000;
  text-decoration: none;
  border-radius: 8px;
  transition: background 0.3s ease;
  font-size: 1rem;
}

.dropdown-link:hover {
  background: #f4f4f9;
}

/* Back-to-Top Button */
.back-to-top {
  position: absolute;
  bottom: 20px;
  right: 20px;
  background: #fff;
  color: #000;
  border: 1px solid #000;
  border-radius: 50%;
  width: 50px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
  transition: background 0.3s ease;
}

.back-to-top:hover {
  background: #f4f4f9;
}

/* Footer Styles */
.footer {
  margin-top: 40px;
  padding: 20px;
  width: 100%;
  text-align: center;
}

.footer-text {
  font-size: 0.9rem;
  color: #333;
  margin: 0;
}

/* Responsive Design */
@media (max-width: 600px) {
  .linktree {
    padding: 10px;
  }

  .profile-image {
    width: 100px;
    height: 100px;
  }

  .profile h1 {
    font-size: 1.8rem;
  }

  .bio {
    font-size: 0.9rem;
  }

  .username {
    font-size: 0.8rem;
  }

  .link-button {
    font-size: 0.9rem;
    padding: 12px;
  }

  .search-bar {
    max-width: 100%;
  }

  .search-input {
    padding: 10px 36px 10px 12px;
    font-size: 0.9rem;
  }

  .search-icon {
    right: 12px;
    font-size: 1rem;
  }

  .back-to-top {
    bottom: 10px;
    right: 10px;
    width: 40px;
    height: 40px;
  }

  .dropdown-content {
    padding: 8px;
  }

  .dropdown-link {
    padding: 8px;
    font-size: 0.9rem;
  }
}
</style>
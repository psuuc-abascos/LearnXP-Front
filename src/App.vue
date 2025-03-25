<template>
  <div class="app-container">
    <!-- Navbar -->
    <nav class="navbar">
      <div class="logo-and-links">
        <div class="logo">
          <img src="./assets/LearnXPLogo.png" alt="LearnXP Logo" class="logo-img" />
          <span class="logo-text">LEARNXP</span>
        </div>
        <!-- Navigation Links (Visible on Desktop) -->
        <div class="nav-links">
          <a href="#" class="nav-link">Discover</a>
          <a href="#" class="nav-link">Marketplace</a>
          <a href="#" class="nav-link">How It Work</a>
        </div>
        <!-- Hamburger Icon for Mobile/Tablet -->
        <button class="hamburger" @click="toggleMenu">
          <span class="hamburger-line"></span>
          <span class="hamburger-line"></span>
          <span class="hamburger-line"></span>
        </button>
        <!-- Navigation Links for Hamburger Menu (Hidden on Desktop) -->
        <div class="nav-links-mobile" :class="{ 'nav-links-active': isMenuOpen }">
          <a href="#" class="nav-link" @click="closeMenu">Discover</a>
          <a href="#" class="nav-link" @click="closeMenu">Marketplace</a>
          <a href="#" class="nav-link" @click="closeMenu">How It Work</a>
          <div class="search-bar-mobile">
            <input type="text" placeholder="Search..." class="search-input" />
            <span class="search-icon">🔍</span>
          </div>
          <button class="connect-wallet-btn" @click="openRoleModal">
            Connect Wallet
          </button>
        </div>
      </div>
      <!-- Right Side: Search Bar and Connect Wallet for Desktop -->
      <div class="right-section">
        <div class="search-bar-desktop">
          <input type="text" placeholder="Search..." class="search-input" />
          <span class="search-icon">🔍</span>
        </div>
        <button class="connect-wallet-btn connect-wallet-desktop" @click="openRoleModal">
          Connect Wallet
        </button>
      </div>
    </nav>

    <!-- Main Section -->
    <main class="main-section">
      <div class="content-left">
        <h1 class="headline">
          Learn, Level Up, and<br />Earn – Where<br />Education Meets<br />Rewards!
        </h1>
        <p class="description">
          LearnXP blends interactive learning with gamification, letting students earn rewards, unlock achievements, and collect NFT badges.
        </p>
      </div>
      <div class="content-right">
        <!-- Pure Image -->
        <img src="./assets/Avatar.png" alt="NFT Avatar" class="avatar-image" />
      </div>
    </main>

    <!-- Role Selection Modal -->
    <div class="modal-overlay" v-if="isRoleModalOpen" @click="closeRoleModal">
      <div class="modal-content" @click.stop>
        <h2 class="modal-title">SELECT YOUR ROLE</h2>
        <div class="role-options">
          <!-- Teacher Role -->
          <div class="role-card" @click="selectRole('Teacher')">
            <img src="./assets/TeacherAvatar.png" alt="Teacher Avatar" class="role-avatar" />
            <p class="role-title">TEACHER #??</p>
            <p class="role-reward">??? LXP</p>
          </div>
          <!-- Student Role -->
          <div class="role-card" @click="selectRole('Student')">
            <img src="./assets/StudentAvatar.png" alt="Student Avatar" class="role-avatar" />
            <p class="role-title">STUDENT #??</p>
            <p class="role-reward">??? LXP</p>
          </div>
        </div>
      </div>
    </div>

    <!-- Registration Modal -->
    <div class="modal-overlay" v-if="isRegistrationModalOpen" @click="closeRegistrationModal">
      <div class="registration-modal-content" @click.stop>
        <h2 class="registration-modal-title">Create An Account</h2>
        <p class="registration-modal-subtitle">
          Sign up to start your gamified learning journey, earn rewards, and unlock achievements!
        </p>
        <form class="registration-form" @submit.prevent="handleRegistration">
          <input
            type="email"
            v-model="registrationForm.email"
            placeholder="Email Address"
            class="registration-input"
            required
          />
          <input
            type="text"
            v-model="registrationForm.name"
            placeholder="Complete Name"
            class="registration-input"
            required
          />
          <input
            type="tel"
            v-model="registrationForm.phone"
            placeholder="Phone Number"
            class="registration-input"
            required
          />
          <input
            type="password"
            v-model="registrationForm.password"
            placeholder="Password"
            class="registration-input"
            required
          />
          <button type="submit" class="create-account-btn">Create Account</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      isMenuOpen: false,
      isRoleModalOpen: false, // State to control the role selection modal
      isRegistrationModalOpen: false, // State to control the registration modal
      selectedRole: null, // Store the selected role
      registrationForm: {
        email: '',
        name: '',
        phone: '',
        password: '',
      },
    };
  },
  methods: {
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen;
    },
    closeMenu() {
      this.isMenuOpen = false;
    },
    openRoleModal() {
      this.isRoleModalOpen = true;
      this.closeMenu(); // Close the hamburger menu if open
    },
    closeRoleModal() {
      this.isRoleModalOpen = false;
    },
    selectRole(role) {
      this.selectedRole = role;
      this.closeRoleModal();
      // Open the registration modal after selecting a role
      this.isRegistrationModalOpen = true;
      console.log(`Selected Role: ${role}`);
    },
    closeRegistrationModal() {
      this.isRegistrationModalOpen = false;
      // Reset the form when closing the modal
      this.registrationForm = {
        email: '',
        name: '',
        phone: '',
        password: '',
      };
    },
    handleRegistration() {
      // Handle the registration logic here
      console.log('Registration Data:', {
        role: this.selectedRole,
        ...this.registrationForm,
      });
      // For now, we'll just close the modal after submission
      this.closeRegistrationModal();
      // Optionally, redirect to a dashboard or perform further actions
      // this.$router.push({ name: `${this.selectedRole}Dashboard` });
    },
  },
};
</script>
<style scoped>
/* General Styles */
.app-container {
  min-height: 100vh;
  background: linear-gradient(135deg, #900777, #181E41);
  color: white;
  font-family: 'Arial', sans-serif;
}

/* Navbar Styles */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.5rem 3rem;
  background: rgba(0, 0, 0, 0.8);
  backdrop-filter: blur(5px);
}

.logo-and-links {
  display: flex;
  align-items: center;
  gap: 2rem;
}

.logo {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.logo-img {
  height: 2.5rem;
}

.logo-text {
  font-size: 1.5rem;
  font-weight: bold;
}

.nav-links {
  display: flex;
  align-items: center;
  gap: 1.5rem;
}

.nav-links-mobile {
  display: none; /* Hidden by default, only shown in hamburger menu */
}

.nav-link {
  color: #d1d5db;
  text-decoration: none;
  font-size: 1rem;
}

.nav-link:hover {
  color: white;
}

/* Right Section (Search Bar and Connect Wallet) */
.right-section {
  display: flex;
  align-items: center;
  gap: 1rem;
}

/* Search Bar Styles */
.search-bar-desktop,
.search-bar-mobile {
  position: relative;
  display: flex;
  align-items: center;
}

.search-input {
  padding: 0.5rem 2rem 0.5rem 1rem;
  border: 1px solid #a855f7;
  border-radius: 9999px;
  background: rgba(255, 255, 255, 0.1);
  color: white;
  font-size: 1rem;
  outline: none;
}

.search-input::placeholder {
  color: #d1d5db;
}

.search-icon {
  position: absolute;
  right: 0.75rem;
  font-size: 1rem;
  color: #d1d5db;
}

.connect-wallet-btn {
  background-color: transparent;
  border: 2px solid #a855f7;
  color: white;
  padding: 0.5rem 1rem;
  border-radius: 9999px;
  font-size: 1rem;
  cursor: pointer;
}

.connect-wallet-btn:hover {
  background-color: #a855f7;
}

/* Hamburger Menu Styles */
.hamburger {
  display: none;
  flex-direction: column;
  gap: 0.3rem;
  background: none;
  border: none;
  cursor: pointer;
}

.hamburger-line {
  width: 1.5rem;
  height: 0.2rem;
  background: white;
  border-radius: 2px;
}

/* Main Section Styles */
.main-section {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 6rem 6rem;
  gap: 2rem;
}

.content-left {
  max-width: 50%;
}

.headline {
  font-size: 3.5rem;
  font-weight: bold;
  line-height: 1.2;
  margin-bottom: 1.5rem;
}

.description {
  font-size: 1.2rem;
  color: #d1d5db;
  line-height: 1.6;
}

.content-right {
  max-width: 40%;
}

/* Avatar Image Styles */
.avatar-image {
  width: 100%;
  height: auto;
  transition: transform 0.3s ease; /* Smooth transition for scaling */
}

.avatar-image:hover {
  transform: scale(1.1); /* Scale up by 10% on hover */
}

/* Modal Styles (Role Selection) */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal-content {
  background: transparent;
  padding: 2rem;
  text-align: center;
  width: 90%;
  max-width: 800px;
}

.modal-title {
  font-size: 2.5rem;
  font-weight: bold;
  margin-bottom: 3rem;
  color: white;
  background: none;
}

.role-options {
  display: flex;
  justify-content: space-around;
  gap: 3rem;
}

.role-card {
  background: #2a2a4a;
  border: 2px solid #a855f7;
  padding: 2rem;
  width: 250px;
  cursor: pointer;
  transition: transform 0.3s ease, border-color 0.3s ease;
  clip-path: polygon(
    0% 0%,
    100% 0%,
    100% 85%,
    85% 100%,
    0% 100%
  );
}

.role-card:hover {
  transform: scale(1.05);
  border-color: #ffffff;
}

.role-avatar {
  width: 100%;
  height: auto;
  margin-bottom: 1rem;
}

.role-title {
  font-size: 1.4rem;
  font-weight: bold;
  color: white;
  margin-bottom: 0.5rem;
}

.role-reward {
  font-size: 1.2rem;
  color: #a855f7;
}

/* Registration Modal Styles */
.registration-modal-content {
  background: #2a2a4a;
  border: 2px solid #a855f7;
  border-radius: 15px;
  padding: 2rem;
  text-align: center;
  width: 90%;
  max-width: 500px;
}

.registration-modal-title {
  font-size: 2rem;
  font-weight: bold;
  color: white;
  margin-bottom: 0.5rem;
}

.registration-modal-subtitle {
  font-size: 1rem;
  color: #d1d5db;
  margin-bottom: 2rem;
}

.registration-form {
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.registration-input {
  padding: 0.75rem;
  border: none;
  border-radius: 8px;
  background: white;
  color: black;
  font-size: 1rem;
  outline: none;
}

.registration-input::placeholder {
  color: #6b7280;
}

.create-account-btn {
  background-color: #a855f7;
  color: white;
  padding: 0.75rem;
  border: none;
  border-radius: 8px;
  font-size: 1rem;
  font-weight: bold;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.create-account-btn:hover {
  background-color: #9333ea;
}

/* Responsive Design */
@media (max-width: 1024px) {
  /* Tablet Responsiveness */
  .modal-content {
    max-width: 600px;
  }

  .modal-title {
    font-size: 2rem;
    margin-bottom: 2rem;
  }

  .role-options {
    gap: 2rem;
  }

  .role-card {
    width: 200px;
    padding: 1.5rem;
  }

  .role-title {
    font-size: 1.2rem;
  }

  .role-reward {
    font-size: 1rem;
  }

  .registration-modal-content {
    max-width: 450px;
  }

  .registration-modal-title {
    font-size: 1.8rem;
  }

  .registration-modal-subtitle {
    font-size: 0.9rem;
  }
}

@media (max-width: 768px) {
  /* Mobile Responsiveness */
  .logo-and-links {
    position: relative;
    width: 100%;
    justify-content: space-between;
  }

  .hamburger {
    display: flex;
  }

  .nav-links {
    display: none;
  }

  .nav-links-mobile {
    display: none;
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    background: rgba(0, 0, 0, 0.9);
    flex-direction: column;
    align-items: flex-start;
    padding: 1rem 3rem;
    gap: 1rem;
    z-index: 10;
  }

  .nav-links-active {
    display: flex;
  }

  .right-section {
    display: none;
  }

  .main-section {
    flex-direction: column;
    padding: 2rem;
  }

  .content-left,
  .content-right {
    max-width: 100%;
  }

  .headline {
    font-size: 2.5rem;
  }

  .avatar-image {
    width: 80%;
    margin: 0 auto;
  }

  .modal-content {
    max-width: 90%;
    padding: 1rem;
  }

  .modal-title {
    font-size: 1.8rem;
    margin-bottom: 1.5rem;
  }

  .role-options {
    flex-direction: column;
    align-items: center;
    gap: 1.5rem;
  }

  .role-card {
    width: 80%;
    max-width: 300px;
    padding: 1.5rem;
  }

  .role-title {
    font-size: 1.2rem;
  }

  .role-reward {
    font-size: 1rem;
  }

  .registration-modal-content {
    max-width: 90%;
    padding: 1.5rem;
  }

  .registration-modal-title {
    font-size: 1.5rem;
  }

  .registration-modal-subtitle {
    font-size: 0.85rem;
  }

  .registration-input {
    padding: 0.5rem;
    font-size: 0.9rem;
  }

  .create-account-btn {
    padding: 0.5rem;
    font-size: 0.9rem;
  }
}
</style>
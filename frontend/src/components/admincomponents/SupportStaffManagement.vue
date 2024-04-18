<template>
  <div>
    <!-- Left-side navigation bar -->
    <div class="sidebar">
      <!-- Admin information -->
      <div class="user-info">
        <!-- Large admin photo -->
        <div class="user-photo">
          <img src="./profile.jpg" alt="Admin Photo" class="rounded-photo">
          <h3>ADMIN</h3>
        </div>
      </div>
      <!-- Navigation links -->
      <div class="navigation-links">
        <ul>
          <li><router-link to='/dashboard'>Home</router-link></li>
          <li><router-link to='/SupportStaffManagement'>Support Staff Management</router-link></li>
          <li><router-link to='/UserManagement'>User Management</router-link></li>
          <li><router-link to='/Requests'>Requests</router-link></li>
        </ul>
      </div>
    </div>
    <!-- Main content area -->
    <div class="main-content">
      <!-- Main user information section -->
      <div class="profile">
        <!-- Navigation bar -->
        <div class="navbar">
          <div class="website-name">{{ websiteName }}</div>
          <router-link to="/"><button @click="logoutUser" class="logout-button">Logout</button></router-link>
        </div>


      </div>
    </div>

    <!-- Main content area -->
    <div class="main-content">
      <!-- Support Staff Management Section -->
      <div class="support-staff-management">
        <!-- Heading -->
        <h2>Support Staff Management</h2>



        <div class="row">
          <div class="card my-2 mx-2 col-6"  style="width: 15rem; background-color:black"
            v-for="(t, index) in supportstaff" :key="index" >
            
              <div class="card-body">
                
                <h5 class="card-title text-danger">Staff ID: {{ t.id }}</h5>
                <h6 class="card-text text-warning">User ID: {{ t.username }}</h6>
                <p class="card-text text-warning">Email ID: {{ t.email }} </p>
                <router-link :to="'/SSManage/'+t.id ">
                  
      <button  class="btn btn-success">Open</button>
    </router-link>
                <!-- <p class="card-text text-success">Tags: {{ t.id }}</p>
                <p class="card-text text-primary">Genre: {{ t.id }}</p> -->
              
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

</template>

<script>
export default {
  name: "SupportStaffManagement",
  data() {
    return {
      supportstaff: "",
      websiteName: "Disntegrate"
    };
  },
  created() {
    this.getAdminHomeData();
    // Refresh data every 2 minutes
    setInterval(() => {
      this.getAdminHomeData();
    }, 30000 * 2);
  },
  methods: {
  getAdminHomeData() {
    fetch('http://localhost:5000/users')
      .then(response => response.json())
      .then(data => {
        // Filter the data based on the role attribute
        this.supportstaff = data.filter(user => user.role === 2);
      })
      .catch(error => {
        console.error('Error fetching admin home data:', error);
      });
  },
  logoutUser() {
    // Implement logout functionality
  }
}
};
</script>

<style scoped>
/* Left-side navigation bar styles */
.sidebar {
  width: 250px;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  background-color: #333;
  color: #fff;
  padding-top: 20px;
}

.user-info {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 0 20px;
  margin-bottom: 20px;
}

.user-photo {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  overflow: hidden;
  margin-bottom: 10px;
}

.rounded-photo {
  width: 100%;
  height: auto;
}

.navigation-links ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
}

.navigation-links ul li {
  padding: 10px 20px;
}

.navigation-links ul li a {
  text-decoration: none;
  color: #fff;
}

.navigation-links ul li a:hover {
  text-decoration: underline;
}

/* Main content area styles */
.main-content {
  margin-left: 250px;
  /* Adjusted to match the width of the sidebar */
  padding: 20px;
}

.support-staff-management {
  text-align: center;
}

.support-staff-management h2 {
  margin-bottom: 20px;
}

.staff-profiles {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.staff-profile {
  width: 200px;
  padding: 10px;
  margin: 10px;
  background-color: #f2f2f2;
  border-radius: 8px;
}

.staff-photo {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  margin-bottom: 10px;
}

/* Main content area styles */
.main-content {
  margin-left: 250px;
  /* Adjusted to match the width of the sidebar */
  padding: 20px;
}

/* Styles for navigation bar */
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px;
  background-color: #f0f0f0;
}

.website-name {
  font-size: 20px;
}

.logout-button {
  background-color: #ff6f61;
  border: none;
  color: white;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.logout-button:hover {
  background-color: #e65346;
}
</style>

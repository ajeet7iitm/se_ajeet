<template>
  <div>
    <!-- Left-side navigation bar -->
    <div class="sidebar">
      <!-- User information -->
      <div class="user-info">
        <!-- Small user photo -->
        <div class="small-user-photo">
          <img src="../profile.jpg" alt="User Photo" class="small-rounded-photo">
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

        <div class="row">
          <h3>Category Requests</h3>

          <div class="card my-2 mx-2 col-6" style="width: 18.5rem; background-color:black"
            v-for="(u, index) in user1.category_request" :key="index">
            <div class="card-body">
              <h5 class="card-title text-danger">User ID: {{ u.user_id }}</h5>
              <h6 class="card-text text-warning">Category: {{ u.category }}</h6>


              <!-- different buttons to get output -->
              <button type="button" class="card-link btn btn-success"
                :data-bs-target="'#staticBackdrop1' + u.user_id + u.category" data-bs-toggle="modal">
                Accept
              </button>
              <button type="button" class="card-link btn btn-danger"
                :data-bs-target="'#staticBackdrop11' + u.user_id + u.category" data-bs-toggle="modal">
                Reject
              </button>



              <!-- Modal for Remove Tags -->
              <div class="modal fade" :id="'staticBackdrop1' + u.user_id + u.category" data-bs-backdrop="static"
                data-bs-keyboard="false" tabindex="-1" :aria-labelledby="'staticBackdropLabel1' + u.user_id + u.category"
                aria-hidden="true">
                <div class="modal-dialog">
                  <div class="modal-content">
                    <div class="modal-header">
                      <h1 class="modal-title fs-5" :id="'staticBackdropLabel1' + u.user_id + u.category">Add
                        Category</h1>
                      <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                      <div class="my-3">
                        <label> Are you sure to add this category! </label>
                      </div>
                    </div>
                    <div class="modal-footer">
                      <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>

                      <button type="button" @click="cat(u.user_id, u.category,res=1,cat1)" class="btn btn-danger"
                        data-bs-dismiss="modal">Add Category</button>
                    </div>
                  </div>
                </div>
              </div>
              <!-- Modal for Remove Tags -->
              <div class="modal fade" :id="'staticBackdrop11' + u.user_id + u.category" data-bs-backdrop="static"
                data-bs-keyboard="false" tabindex="-1"
                :aria-labelledby="'staticBackdropLabel11' + u.user_id + u.category" aria-hidden="true">
                <div class="modal-dialog">
                  <div class="modal-content">
                    <div class="modal-header">
                      <h1 class="modal-title fs-5" :id="'staticBackdropLabel11' + u.user_id + u.category">Reject
                        Category</h1>
                      <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                      <div class="my-3">
                        <label> Are you sure to reject this category! </label>
                      </div>
                    </div>
                    <div class="modal-footer">
                      <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>

                      <button type="button" @click="cat(u.user_id, u.category, res = -1,cat1)" class="btn btn-danger"
                        data-bs-dismiss="modal">Reject Category</button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <div class="row">
          <h3>FAQ Requests</h3>
          <div class="card my-2 mx-2 col-6" style="width: 18.5rem; background-color:black"
            v-for="(c, index) in user1.faq_request" :key="index">
            <div class="card-body">

              <!-- <h5 class="card-title text-danger">Staff ID: {{ c.staff_id }}</h5> -->
              <h6 class="card-text text-warning">Topic ID: {{ c.topic_id }}</h6>
              <h6 class="card-text text-warning">Solution ID:{{ c.solution_post_it }}</h6>


              <!-- different buttons to get output -->
              <button type="button" class="card-link btn btn-success" :data-bs-target="'#staticBackdrop2' + c.solution_post_it+c.topic_id"
                data-bs-toggle="modal">
                Accept
              </button>
              <button type="button" class="card-link btn btn-danger" :data-bs-target="'#staticBackdrop22' + c.solution_post_it+c.topic_id"
                data-bs-toggle="modal">
                Reject
              </button>



              <!-- Modal for Remove Tags -->
              <div class="modal fade" :id="'staticBackdrop2' + c.solution_post_it+c.topic_id" data-bs-backdrop="static"
                data-bs-keyboard="false" tabindex="-1" :aria-labelledby="'staticBackdropLabel2' + c.solution_post_it+c.topic_id"
                aria-hidden="true">
                <div class="modal-dialog">
                  <div class="modal-content">
                    <div class="modal-header">
                      <h1 class="modal-title fs-5" :id="'staticBackdropLabel2' + c.solution_post_it+c.topic_id">Accept FAQ</h1>
                      <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                      <div class="my-3">
                        <label> Are you sure to accept this FAQ! </label>
                      </div>
                    </div>
                    <div class="modal-footer">
                      <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                      <button type="button" @click="cat( c.solution_post_it,c.topic_id,res=1,faq1)" class="btn btn-danger"
                        data-bs-dismiss="modal">Accept FAQ</button>
                    </div>
                  </div>
                </div>
              </div>
              <!-- Modal for Remove Tags -->
              <div class="modal fade" :id="'staticBackdrop22' + c.solution_post_it+c.topic_id" data-bs-backdrop="static"
                data-bs-keyboard="false" tabindex="-1" :aria-labelledby="'staticBackdropLabel22' + c.solution_post_it+c.topic_id"
                aria-hidden="true">
                <div class="modal-dialog">
                  <div class="modal-content">
                    <div class="modal-header">
                      <h1 class="modal-title fs-5" :id="'staticBackdropLabel22' + c.solution_post_it+c.topic_id">Reject FAQ</h1>
                      <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body">
                      <div class="my-3">
                        <label> Are you sure to reject this FAQ! </label>
                      </div>
                    </div>
                    <div class="modal-footer">
                      <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                      <button type="button" @click="cat(c.solution_post_it,c.topic_id,res=-1,faq1)" class="btn btn-danger"
                        data-bs-dismiss="modal">Reject FAQ</button>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
export default {
  name: "RaisedRequests",
  data() {
    return {
      res: "",
      cat1:"category",
      faq1:"faq",
      user1: [],
      catall: [],
      websiteName: "Disintegrate"
    };
  },
  methods: {
    logoutUser() {
      // Your logout logic here
      console.log("Logout clicked");
    },
    cat(a,b,c,d) {
      const data = {
        section:d,
        sid: a,
        ctid: b,
        response:c
      };
console.log(data)
      fetch(`http://localhost:5000/api/admin/adminpostrequest`, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(data),
      })
        .then((response) => {
          if (!response.ok) {
            throw new Error('Failed to revoke category');
          }
          return response.json();
        })
        .then((data) => {
          console.log("Success:", data);
          // Fetch updated cat data
          this.fetchCatData();
        })
        .catch((error) => {
          console.error("Error:", error);
        });
    },
    fetchCatData() {
      // Fetch updated cat data
      fetch("http://localhost:5000/api/admin/admingetrequest")
        .then((response) => response.json())
        .then((data) => {
          console.log("Cat data returned from the backend:", data);
          this.user1 = data;
        });
    },
  },
  mounted() {
    // Fetch user data
    fetch("http://localhost:5000/api/admin/admingetrequest")
      .then((response) => response.json())
      .then((data) => {
        console.log("Data returned from the backend:", data);
        this.user1 = data;
      });

    // Fetch cat data
    this.fetchCatData();
  },
};
</script>


<style scoped>
/* Styles here */
</style>


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

.small-user-photo {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  overflow: hidden;
}

.small-rounded-photo {
  width: 100%;
  height: auto;
}

.username {
  margin-top: 10px;
  font-size: 18px;
}

.edit-profile-button {
  background-color: #4CAF50;
  border: none;
  color: white;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
  margin-top: 10px;
}

.edit-profile-button:hover {
  background-color: #45a049;
}

.user-email {
  margin-top: 10px;
  font-size: 14px;
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

/* Main user info layout */
.main-user-info {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.user-details {
  display: flex;
  align-items: center;
}

.user-photo {
  width: 150px;
  height: 150px;
  border-radius: 50%;
  overflow: hidden;
  margin-right: 20px;
}

.rounded-photo {
  width: 100%;
  height: auto;
}

.name-email {
  text-align: center;
}

.name-email h2 {
  margin-top: 0;
}

.name-email .email {
  margin-bottom: 10px;
}

/* Allotted tags */
.allotted-tags {
  margin-top: 20px;
  text-align: center;
}

.allotted-tags p {
  margin-bottom: 5px;
}

.allotted-tags ul {
  list-style-type: none;
  padding: 0;
  margin: 0;
  display: flex;
  /* Display as horizontal list */
  justify-content: center;
  /* Center align the tags */
}

.allotted-tags ul li {
  margin-right: 10px;
  /* Add spacing between tags */
  background-color: #007bff;
  color: #fff;
  padding: 5px 10px;
  border-radius: 20px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.allotted-tags ul li:hover {
  background-color: #0056b3;
}

/* User stats layout */
.user-stats {
  margin-top: 20px;
  display: flex;
  justify-content: space-around;
}

.stat {
  margin-bottom: 10px;
}

.stat-label {
  font-weight: bold;
}

.stat-value {
  margin-left: 10px;
}
</style>
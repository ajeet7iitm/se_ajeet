<template>
    <div>
      <SideBarComponent :user="user" />
      <NavBarComponent />
      <div class="notification-container">
        <div class="search-box">
          <input type="text" placeholder="Search here" class="search-input" v-model="searchText">
          <button class="filter-button">Filter</button>
        </div>
        <div class="notification-text">Frequently Asked Questions</div>

      <!-- Loop through rows -->
      <div class="notification-row" v-for="(row, index) in rows" :key="index">
        <!-- Loop through columns -->
        <button class="notification-button" v-for="(column, colIndex) in row" :key="colIndex">
          <button class="inner-button" v-text="column"></button>
        </button>
      </div>
      </div>
    </div>
  </template>
  
  <script>
  import SideBarComponent from "../SideBarComponent.vue";
  import NavBarComponent from ".../generalcomponents/NavBarComponent.vue";
  
  export default {
    name: "QuestionsComponent",
    components: {
      SideBarComponent,
      NavBarComponent,
    },
    data() {
      return {
        user: {
          name: "John Doe",
          // Hardcoded user photo path
          photo: "../user-photo.jpg", // Example URL for user photo
          bio: "Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed dapibus elit eu convallis eleifend.",
          email: "john.doe@example.com"
        },
        searchText: '',
        rows: [
        ["How to add calendar schedule?", "→"],
        ["How to report a user?", "→"],
        ["How to login to seek portal?", "→"],
        ["How to turn on camera?", "→"],
        ["How to drop a subject?", "→"]
      ]
      };
    }
  };
  </script>
  
  <style scoped>
  .notification-container {
    padding: 20px;
    background-color: #f0f0f0;
    margin-left: 250px; /* Adjusted to match the width of the sidebar */
  }
  
  .search-box {
    display: flex;
    align-items: center;
    margin-bottom: 20px;
  }
  
  .search-input {
    flex: 1;
    padding: 5px;
    border: 1px solid #ccc;
    border-radius: 5px;
    margin-right: 10px;
  }
  
  .filter-button {
    padding: 5px 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    cursor: pointer;
  }
  
  .notification-text {
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 10px;
  }
  
  .notification-button {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0;
  border: none;
  background: none;
  cursor: pointer;
}

.notification-button .inner-button {
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  cursor: pointer;
}

.notification-button .inner-button.text {
  flex: 1;
}

.notification-button .inner-button.arrow {
  margin: 0 10px;
}

.notification-button .inner-button.date {
  font-size: 12px;
}
.notification-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 10px;
    background-color: #ddd;
    border: 1px solid #ccc;
    border-radius: 5px;
    margin-bottom: 10px;
}

.header-column {
    flex: 1;
    text-align: center;
}

.notification-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 10px;
}

.notification-row .notification-button {
    width: 100%;
}
  </style>
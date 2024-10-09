# Sibasi Academy - Application Form Project

This project is a simple web application for the Sibasi Academy application form. It includes a login form, a dashboard, a ToDo list, and a responsive page with text cards. The project is built using HTML, CSS, and JavaScript.

## Features

1. **Login Form**
   - Validates that the email is in the correct format.
   - Ensures the password is more than 8 characters long.
   - Disables the submit button if validation fails.
   - Redirects to a dashboard page upon successful login.

2. **Home Page**
   - Displays a ToDo list where users can add, update, and delete tasks.
   - Tasks are not saved and will be cleared on page reload.

3. **Second Page**
   - Shows text cards that are responsive to desktop, tablet, and mobile views.
   - On desktop: 3 cards aligned horizontally.
   - On tablet: 2 cards aligned horizontally with the third card below.
   - On mobile: Cards aligned vertically.

## Project Structure


## Getting Started

### Prerequisites

- A web browser.
- Basic understanding of HTML, CSS, and JavaScript.

### Running the Project

1. Clone the repository or download the project files.
2. Open `index.html` in your web browser to view the application.

## JavaScript Code Explanation

### `script.js`

The `script.js` file contains the main functionality of the web application. Below is a detailed explanation of the JavaScript code:

```js
// Wait for the DOM to be fully loaded before executing the script
document.addEventListener('DOMContentLoaded', () => {
  const content = document.getElementById('content');
  const homeLink = document.getElementById('home-link');
  const secondLink = document.getElementById('second-link');

  // Function to display the login page
  const showLoginPage = () => {
    content.innerHTML = `
      <div class="container">
        <form id="login-form">
          <h2>Login</h2>
          <div class="form-group">
            <label>Email:</label>
            <input type="email" id="email" required>
          </div>
          <div class="form-group">
            <label>Password:</label>
            <input type="password" id="password" required>
          </div>
          <button type="submit" id="submit-button" disabled>Submit</button>
        </form>
      </div>
    `;

    const emailInput = document.getElementById('email');
    const passwordInput = document.getElementById('password');
    const submitButton = document.getElementById('submit-button');

    // Function to validate the login form
    const validateForm = () => {
      const email = emailInput.value;
      const password = passwordInput.value;
      const emailRegex = /\S+@\S+\.\S+/;
      // Enable submit button if email is valid and password is more than 8 characters long
      if (emailRegex.test(email) && password.length > 8) {
        submitButton.disabled = false;
      } else {
        submitButton.disabled = true;
      }
    };

    // Add input event listeners to validate form in real-time
    emailInput.addEventListener('input', validateForm);
    passwordInput.addEventListener('input', validateForm);

    // Handle form submission
    document.getElementById('login-form').addEventListener('submit', (e) => {
      e.preventDefault(); // Prevent default form submission
      showDashboardPage(); // Show the dashboard page on successful login
    });
  };

  // Function to display the dashboard page
  const showDashboardPage = () => {
    content.innerHTML = `
      <div class="container">
        <h1>Welcome to the Dashboard</h1>
      </div>
    `;
  };

  // Function to display the home page with a ToDo list
  const showHomePage = () => {
    content.innerHTML = `
      <div class="container">
        <h2>ToDo List</h2>
        <div class="add-task">
          <input type="text" id="new-task" placeholder="Add a new task">
          <button id="add-task-button">Add</button>
        </div>
        <ul class="task-list" id="task-list"></ul>
      </div>
    `;

    const taskList = document.getElementById('task-list');
    const newTaskInput = document.getElementById('new-task');
    const addTaskButton = document.getElementById('add-task-button');

    // Function to add a task to the ToDo list
    const addTask = () => {
      const taskText = newTaskInput.value.trim();
      if (taskText) {
        const taskItem = document.createElement('li');
        taskItem.innerHTML = `
          <input type="text" value="${taskText}" readonly>
          <button class="delete-task-button">Delete</button>
        `;
        taskList.appendChild(taskItem); // Add task to the list
        newTaskInput.value = ''; // Clear the input field
      }
    };

    // Add event listener to the Add Task button
    addTaskButton.addEventListener('click', addTask);

    // Handle task deletion
    taskList.addEventListener('click', (e) => {
      if (e.target.classList.contains('delete-task-button')) {
        e.target.parentElement.remove();
      }
    });
  };

  // Function to display the second page with a responsive card layout
  const showSecondPage = () => {
    content.innerHTML = `
      <div class="container cards">
        <div class="card">Card 1</div>
        <div class="card">Card 2</div>
        <div class="card">Card 3</div>
      </div>
    `;
  };

  // Add event listeners to the navigation links
  homeLink.addEventListener('click', (e) => {
    e.preventDefault(); // Prevent default link behavior
    showHomePage(); // Show the home page
  });

  secondLink.addEventListener('click', (e) => {
    e.preventDefault(); // Prevent default link behavior
    showSecondPage(); // Show the second page
  });

  // Initially show the login page
  showLoginPage();
});

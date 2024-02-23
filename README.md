Certainly! Below is a simple example using HTML, CSS, and JavaScript to implement the described functionality. Please note that this is a basic example and may need to be adapted to fit into a specific web application framework.

**HTML (index.html):**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="styles.css">
  <title>Login Page</title>
</head>
<body>
  <button id="loginButton">Login</button>

  <script src="script.js"></script>
</body>
</html>
```

**CSS (styles.css):**

```css
body {
  font-family: Arial, sans-serif;
  text-align: center;
  padding: 20px;
}

button {
  font-size: 16px;
  padding: 10px;
  cursor: pointer;
}
```

**JavaScript (script.js):**

```javascript
// Check if user session exists
const userSession = sessionStorage.getItem('userSession');

// Check if user color preference exists
const userColor = localStorage.getItem('userColor');

// Redirect functions
function redirectToDashboard() {
  window.location.href = 'dashboard.html';
}

function redirectToLogin() {
  window.location.href = 'index.html';
}

// Event listener for login button
document.getElementById('loginButton').addEventListener('click', function() {
  if (userSession) {
    redirectToDashboard();
  } else {
    // Set user session on login
    sessionStorage.setItem('userSession', true);
    redirectToDashboard();
  }
});

// Check if on dashboard page
if (window.location.href.includes('dashboard.html')) {
  // Redirect to login if no user session
  if (!userSession) {
    redirectToLogin();
  }

  // Set background color if user has a color preference
  if (userColor) {
    document.body.style.backgroundColor = userColor;
  }

  // Event listener for color buttons
  document.addEventListener('DOMContentLoaded', function() {
    const colorButtons = document.querySelectorAll('.color-button');

    colorButtons.forEach(function(button) {
      button.addEventListener('click', function() {
        const color = this.getAttribute('data-color');
        document.body.style.backgroundColor = color;

        // Save user color preference
        localStorage.setItem('userColor', color);
      });
    });
  });

  // Event listener for page refresh
  window.addEventListener('beforeunload', function() {
    // Clear user color preference on new tab
    localStorage.removeItem('userColor');
  });
}
```

**HTML (dashboard.html):**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="styles.css">
  <title>Dashboard</title>
</head>
<body>
  <h1>Welcome to the Dashboard!</h1>
  <button class="color-button" data-color="red">Red</button>
  <button class="color-button" data-color="blue">Blue</button>
  <button class="color-button" data-color="green">Green</button>

  <script src="script.js"></script>
</body>
</html>
```

This example should give you a basic framework to implement the described functionality. Adjustments might be needed based on the specifics of your web application.

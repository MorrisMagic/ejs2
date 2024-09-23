const express = require('express');
const path = require('path');

const app = express();

const checkWorkingHours = (req, res, next) => {
  const currentDateTime = new Date();
  const day = currentDateTime.getDay();
  const hour = currentDateTime.getHours();

  if (day >= 1 && day <= 5 && hour >= 9 && hour < 17) {
    next(); // Within working hours, continue
  } else {
    res.send('<h1>Sorry, our website is available only during working hours (Monday to Friday, 9am to 5pm).</h1>');
  }
};

app.set('view engine', 'ejs');

app.use(checkWorkingHours);

app.use(express.static(path.join(__dirname, 'public')));

app.get('/', (req, res) => {
  res.render('index', { pageTitle: 'Home' });
});

app.get('/services', (req, res) => {
  res.render('services', { pageTitle: 'Our Services' });
});

app.get('/contact', (req, res) => {
  res.render('contact', { pageTitle: 'Contact Us' });
});

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server is running on port ${PORT}`);
});


// index
<html>
<head>
  <title><%= pageTitle %></title>
  <link rel="stylesheet" href="/styles.css">
</head>
<body>
  <nav>
    <a href="/">Home</a>
    <a href="/services">Our Services</a>
    <a href="/contact">Contact Us</a>
  </nav>
  <h1>Welcome to Our Home Page</h1>
</body>
</html>

<html>
<head>
  <title><%= pageTitle %></title>
  <link rel="stylesheet" href="/styles.css">
</head>
<body>
  <nav>
    <a href="/">Home</a>
    <a href="/services">Our Services</a>
    <a href="/contact">Contact Us</a>
  </nav>
  <h1>Our Services</h1>
  <p>Here we offer a variety of services to meet your needs!</p>
</body>
</html>

<html>
<head>
  <title><%= pageTitle %></title>
  <link rel="stylesheet" href="/styles.css">
</head>
<body>
  <nav>
    <a href="/">Home</a>
    <a href="/services">Our Services</a>
    <a href="/contact">Contact Us</a>
  </nav>
  <h1>Contact Us</h1>
  <p>Feel free to reach out to us via email or phone!</p>
</body>
</html>



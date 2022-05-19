- 👋 Hi, I’m @harish9012
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
harish9012/harish9012 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->



const Joi = require('joi');
const express = require('express');
const app = express();

app.use(express.json());

const genres = [
  { id: 1, name: 'Action' },  
  { id: 2, name: 'Horror' },  
  { id: 3, name: 'Romance' },  
];
app.get('/api/genres', (req, res) => {
  res.send(genres);
});

app.post('/api/genres', (req, res) => {
  const { error } = validateGenre(req.body); 
  if (error) return res.status(400).send(error.details[0].message);

  const genre = {
    id: genres.length + 1,
    name: req.body.name
  };
  genres.push(genre);
  res.send(genre);
});

app.put('/api/genres/:id', (req, res) => {
  const genre = genres.find(c => c.id === parseInt(req.params.id));
  if (!genre) return res.status(404).send('The genre with the given ID was not found.');

  const { error } = validateGenre(req.body); 
  if (error) return res.status(400).send(error.details[0].message);
  
  genre.name = req.body.name; 
  res.send(genre);
});

app.delete('/api/genres/:id', (req, res) => {
  const genre = genres.find(c => c.id === parseInt(req.params.id));
  if (!genre) return res.status(404).send('The genre with the given ID was not found.');

  const index = genres.indexOf(genre);
  genres.splice(index, 1);

  res.send(genre);
});

app.get('/api/genres/:id', (req, res) => {
  const genre = genres.find(c => c.id === parseInt(req.params.id));
  if (!genre) return res.status(404).send('The genre with the given ID was not found.');
  res.send(genre);
});

function validateGenre(genre) {
  const schema = {
    name: Joi.string().min(3).required()
  };

  return Joi.validate(genre, schema);
}

const port = process.env.PORT || 3000;
app.listen(port, () => console.log(`Listening on port ${port}...`));




























const Joi = require('joi');
const express = require('express');
const app = express();

app.use(express.json());

const genres = [
  { id: 1, name: 'Action' },  
  { id: 2, name: 'Horror' },  
  { id: 3, name: 'Romance' },  
];

app.get('/api/genres', (req, res) => {
  res.send(genres);
});

app.post('/api/genres', (req, res) => {
  const { error } = validateGenre(req.body); 
  if (error) return res.status(400).send(error.details[0].message);

  const genre = {
    id: genres.length + 1,
    name: req.body.name
  };
  genres.push(genre);
  res.send(genre);
});

app.put('/api/genres/:id', (req, res) => {
  const genre = genres.find(c => c.id === parseInt(req.params.id));
  if (!genre) return res.status(404).send('The genre with the given ID was not found.');

  const { error } = validateGenre(req.body); 
  if (error) return res.status(400).send(error.details[0].message);
  
  genre.name = req.body.name; 
  res.send(genre);
});

app.delete('/api/genres/:id', (req, res) => {
  const genre = genres.find(c => c.id === parseInt(req.params.id));
  if (!genre) return res.status(404).send('The genre with the given ID was not found.');

  const index = genres.indexOf(genre);
  genres.splice(index, 1);

  res.send(genre);
});

app.get('/api/genres/:id', (req, res) => {
  const genre = genres.find(c => c.id === parseInt(req.params.id));
  if (!genre) return res.status(404).send('The genre with the given ID was not found.');
  res.send(genre);
});

function validateGenre(genre) {
  const schema = {
    name: Joi.string().min(3).required()
  };

  return Joi.validate(genre, schema);
}

const port = process.env.PORT || 3000;
app.listen(port, () => console.log(`Listening on port ${port}...`));















const express = require(‘express’);

const path = require(‘path’);

const port = 8000;

const app = express();

app.set(‘view engine’, ‘ejs’);

app.set(‘views’, path.join(__dirname, ‘views’));

app.use(express.urlencoded());

app.use(express.static(‘assets’));

var contactList = [

{

id : “1”,

name: “Harish”,

phone: “1111111111”

},

{

id : “2”,

name: “Tony Stark”,

phone: “1234567890”

},

{

id : “3”,

name: “Node Express”,

phone: “12131321321”

}

]

app.get(‘/practice’, function(req, res){

return res.render(‘practice’, {

title: “Let us play with ejs”

});

});

app.get(‘/’, function(req, res){

return res.render(‘home’,{

title: “Contact List”,

contact_list: contactList

});

})

app.post(‘/create-contact’, function(req, res){

console.log(“{“,req.body.name,”:”,req.body.phone);

contactList.push(req.body);

return res.redirect(‘/’);

});

app.listen(port, function(err){

if (err) {

console.log(“Error in running the server”, err);

}

console.log(‘Yup!My Server is running on Port’, port);

})

app.get(‘/delete-contact/’, function(req, res){

console.log(req.body);

let fid = req.body.id

// let del = contactList.filter(getdata);

// function getdata(item){

// return item.phone !== phone

// }

let contactindex = contactList.findIndex(contact => contact.id == fid);

if(contactindex != -1){

contactList.splice(contactindex, 1);

}

return res.redirect(‘back’);

});

import fetch from ‘node-fetch’

fetch(‘http://localhost:3000/api/genres').then((res)=>res.json()).then((val)=>console.log(val))

<html>

<head>

<title>

<%= locals.title%>

</title>

<link rel=”stylesheet” href=”/css/home.css”>

</head>

<body>

<div>

<ul>

<% for (let i of contact_list) { %>

<div class=”contact”>

<li>

<p><%= i.id %></p>

<p><%= i.name %></p>

<p><%= i.phone %></p>

</li>

</div>

<div class=”delete-button”>

<a href=”/delete-contact/?id=<%= i.id %>”>

delete

</a>

</div>

<% } %>

</ul>

</div>

<form action=”/create-contact” method=”POST”>

<input type=”text” name=”name” id = “uname” placeholder=”Enter name” required>

<input type=”number” name=”phone” id = “unum”placeholder=”Enter phone” required>

<h1 id = “values”></h1>

<button type=”submit”>Add contact</button>

</form>

<! — <script type=”text/javascript” src=”/js/home.js”></script> →

<script>

const input = document.querySelector(‘#unum’);

const log = document.getElementById(‘values’);

input.addEventListener(‘input’, updateValue);

function updateValue(e) {

log.textContent = e.target.value;

}

document.getElementById(‘check’).innerHTML = data

</script>

</body>

</html>

const Joi = require(‘joi’);

const express = require(‘express’);

const app = express();

app.use(express.json());

const genres = [

{ id: 1, name: ‘Action’ },

{ id: 2, name: ‘Horror’ },

{ id: 3, name: ‘Romance’ },

];

app.get(‘/api/genres’, (req, res) => {

res.send(genres);

});

app.post(‘/api/genres’, (req, res) => {

const { error } = validateGenre(req.body);

if (error) return res.status(400).send(error.details[0].message);

const genre = {

id: genres.length + 1,

name: req.body.name

};

genres.push(genre);

res.send(genre);

});

app.put(‘/api/genres/:id’, (req, res) => {

const genre = genres.find(c => c.id === parseInt(req.params.id));

if (!genre) return res.status(404).send(‘The genre with the given ID was not found.’);

const { error } = validateGenre(req.body);

if (error) return res.status(400).send(error.details[0].message);

genre.name = req.body.name;

res.send(genre);

});

app.delete(‘/api/genres/:id’, (req, res) => {

const genre = genres.find(c => c.id === parseInt(req.params.id));

if (!genre) return res.status(404).send(‘The genre with the given ID was not found.’);

const index = genres.indexOf(genre);

genres.splice(index, 1);

res.send(genre);

});

app.get(‘/api/genres/:id’, (req, res) => {

const genre = genres.find(c => c.id === parseInt(req.params.id));

if (!genre) return res.status(404).send(‘The genre with the given ID was not found.’);

res.send(genre);

});

function validateGenre(genre) {

const schema = {

name: Joi.string().min(3).required()

};

return Joi.validate(genre, schema);

}

const port = process.env.PORT || 3000;

app.listen(port, () => console.log(`Listening on port ${port}…`));

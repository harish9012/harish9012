- š Hi, Iām @harish9012
- š Iām interested in ...
- š± Iām currently learning ...
- šļø Iām looking to collaborate on ...
- š« How to reach me ...

<!---
harish9012/harish9012 is a āØ special āØ repository because its `README.md` (this file) appears on your GitHub profile.
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















const express = require(āexpressā);

const path = require(āpathā);

const port = 8000;

const app = express();

app.set(āview engineā, āejsā);

app.set(āviewsā, path.join(__dirname, āviewsā));

app.use(express.urlencoded());

app.use(express.static(āassetsā));

var contactList = [

{

id : ā1ā,

name: āHarishā,

phone: ā1111111111ā

},

{

id : ā2ā,

name: āTony Starkā,

phone: ā1234567890ā

},

{

id : ā3ā,

name: āNode Expressā,

phone: ā12131321321ā

}

]

app.get(ā/practiceā, function(req, res){

return res.render(āpracticeā, {

title: āLet us play with ejsā

});

});

app.get(ā/ā, function(req, res){

return res.render(āhomeā,{

title: āContact Listā,

contact_list: contactList

});

})

app.post(ā/create-contactā, function(req, res){

console.log(ā{ā,req.body.name,ā:ā,req.body.phone);

contactList.push(req.body);

return res.redirect(ā/ā);

});

app.listen(port, function(err){

if (err) {

console.log(āError in running the serverā, err);

}

console.log(āYup!My Server is running on Portā, port);

})

app.get(ā/delete-contact/ā, function(req, res){

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

return res.redirect(ābackā);

});

import fetch from ānode-fetchā

fetch(āhttp://localhost:3000/api/genres').then((res)=>res.json()).then((val)=>console.log(val))

<html>

<head>

<title>

<%= locals.title%>

</title>

<link rel=āstylesheetā href=ā/css/home.cssā>

</head>

<body>

<div>

<ul>

<% for (let i of contact_list) { %>

<div class=ācontactā>

<li>

<p><%= i.id %></p>

<p><%= i.name %></p>

<p><%= i.phone %></p>

</li>

</div>

<div class=ādelete-buttonā>

<a href=ā/delete-contact/?id=<%= i.id %>ā>

delete

</a>

</div>

<% } %>

</ul>

</div>

<form action=ā/create-contactā method=āPOSTā>

<input type=ātextā name=ānameā id = āunameā placeholder=āEnter nameā required>

<input type=ānumberā name=āphoneā id = āunumāplaceholder=āEnter phoneā required>

<h1 id = āvaluesā></h1>

<button type=āsubmitā>Add contact</button>

</form>

<! ā <script type=ātext/javascriptā src=ā/js/home.jsā></script> ā

<script>

const input = document.querySelector(ā#unumā);

const log = document.getElementById(āvaluesā);

input.addEventListener(āinputā, updateValue);

function updateValue(e) {

log.textContent = e.target.value;

}

document.getElementById(ācheckā).innerHTML = data

</script>

</body>

</html>

const Joi = require(ājoiā);

const express = require(āexpressā);

const app = express();

app.use(express.json());

const genres = [

{ id: 1, name: āActionā },

{ id: 2, name: āHorrorā },

{ id: 3, name: āRomanceā },

];

app.get(ā/api/genresā, (req, res) => {

res.send(genres);

});

app.post(ā/api/genresā, (req, res) => {

const { error } = validateGenre(req.body);

if (error) return res.status(400).send(error.details[0].message);

const genre = {

id: genres.length + 1,

name: req.body.name

};

genres.push(genre);

res.send(genre);

});

app.put(ā/api/genres/:idā, (req, res) => {

const genre = genres.find(c => c.id === parseInt(req.params.id));

if (!genre) return res.status(404).send(āThe genre with the given ID was not found.ā);

const { error } = validateGenre(req.body);

if (error) return res.status(400).send(error.details[0].message);

genre.name = req.body.name;

res.send(genre);

});

app.delete(ā/api/genres/:idā, (req, res) => {

const genre = genres.find(c => c.id === parseInt(req.params.id));

if (!genre) return res.status(404).send(āThe genre with the given ID was not found.ā);

const index = genres.indexOf(genre);

genres.splice(index, 1);

res.send(genre);

});

app.get(ā/api/genres/:idā, (req, res) => {

const genre = genres.find(c => c.id === parseInt(req.params.id));

if (!genre) return res.status(404).send(āThe genre with the given ID was not found.ā);

res.send(genre);

});

function validateGenre(genre) {

const schema = {

name: Joi.string().min(3).required()

};

return Joi.validate(genre, schema);

}

const port = process.env.PORT || 3000;

app.listen(port, () => console.log(`Listening on port ${port}ā¦`));

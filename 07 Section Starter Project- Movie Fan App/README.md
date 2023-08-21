> PARADIGM: "Open Book Exam" aka Reference module-docs mentality

#### 35. [Project Overview](#35)

#### 36. [API key and link for the next lecture](#36)

#### 37. [Project Setup](#37)

#### 38. [Adding the request module](#38)

#### 39. [Putting the data in the template](#39)

#### 40. [Adding the single-movie view](#40)

#### 41. [Adding the search feature](#41)

---

<br>

### 35. Project Overview<a id="35"></a>

<br>

### 36. API key and link for the next lecture<a id="36"></a>

```js
const apiKey = "1fb720b97cc13e580c2c35e1138f90f8";
const apiBaseUrl = "http://api.themoviedb.org/3";
const nowPlayingUrl = `${apiBaseUrl}/most_popular?api_key=${apiKey}`;
const imageBaseUrl = "http://image.tmdb.org/t/p/w300";
```

<br>

### 37. Project Setup<a id="37"></a>

- Generate project Scaffold

```sh
express movieFanSite --view=ejs
cd movieFanSite
npm install
nodemon
```

- localhost "http://localhost:3000/"

---

- remove routes/user.js file
- In app.js remove users import, setup helmet

```js
var createError = require("http-errors");
var express = require("express");
var path = require("path");
var cookieParser = require("cookie-parser");
var logger = require("morgan");

var indexRouter = require("./routes/index");
// 1. var usersRouter = require('./routes/users'); //---remove

var app = express();
// 3. setup helmet
const helmet = require("helmet");
app.use(helmet());

// view engine setup
app.set("views", path.join(__dirname, "views"));
app.set("view engine", "ejs");

app.use(logger("dev"));
app.use(express.json());
app.use(express.urlencoded({ extended: false }));
app.use(cookieParser());
app.use(express.static(path.join(__dirname, "public")));

app.use("/", indexRouter);
// 2. app.use("/users", usersRouter);  // ---remove

// catch 404 and forward to error handler
app.use(function (req, res, next) {
  next(createError(404));
});

// error handler
app.use(function (err, req, res, next) {
  // set locals, only providing error in development
  res.locals.message = err.message;
  res.locals.error = req.app.get("env") === "development" ? err : {};

  // render the error page
  res.status(err.status || 500);
  res.render("error");
});

module.exports = app;
```

---

- stop server, install helmet

```sh
npm i helmet --save
nodemon
```

---

- FRONTEND setup
- In public/stylesheets/style.css copy & paste style from resource

```css
body {
  padding: 10px;
  font: 14px "Lucida Grande", Helvetica, Arial, sans-serif;
}

a {
  color: #00b7ff;
}

.navbar-right {
  margin-right: 10px;
}

.poster img {
  width: 90%;
  text-align: center;
  margin: 10px 5% 10px;
}

#search-form input {
  margin: 8px 0px;
  padding: 5px;
}

.form-group select {
  min-width: 150px;
}

.single-movie-title,
.overview-header {
  font-family: "Metamorphous", cursive;
}

.overview-header {
  font-size: 20px;
  font-weight: bold;
}

.single-movie-overview {
  font-family: "Swanky and Moo Moo", cursive;
  font-size: 24px;
  font-weight: normal;
}
```

---

- In views folder create head.ejs, copy & paste header from resource

```html
<!-- boothstrap cdn -->
<link
  rel="stylesheet"
  href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css"
  integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u"
  crossorigin="anonymous"
/>

<!-- jquery -->
<script src="https://ajax.googleapis.com/ajax/libs/jquery/3.2.1/jquery.min.js"></script>

<!-- Latest compiled and minified JavaScript -->
<!-- boothstrap cdn for modal-->
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>

<!-- google font cdn-->
<link
  href="https://fonts.googleapis.com/css?family=Metamorphous|Swanky+and+Moo+Moo"
  rel="stylesheet"
/>

<!-- local style sheet -->
<link rel="stylesheet" href="/stylesheets/style.css" />
```

---

- In views/index.ejs file, copy & paste from resource

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Movie App</title>

    <!-- include head.ejs partial from view folder  -->
    <!-- Include head means, go and fetch this partial
	     it'll be just like taking this copying and pasting it right here  
		 in place of include head ejs  -->
    <% include head %>
  </head>

  <body>
    <!-- include navbar.ejs partial from view folder -->
    <% include navbar %>

    <div class="container">
      <div class="row">
        <div class="col-sm-12">
          <h1></h1>
        </div>
        <div class="col-sm-12"></div>
      </div>
    </div>
  </body>
</html>
```

---

- In views folder create navbar.ejs, copy & paste navbar from resource

```html
<!-- Boothstrap navbar from w3skool -->

<nav class="navbar navbar-default">
  <div class="container-fluid">
    <div class="navbar-header">
      <a class="navbar-brand" href="/">The New IMDB</a>
    </div>
    <ul class="nav navbar-nav">
      <li><a href="/login">Login</a></li>
      <li><a href="/favorites">Favorites</a></li>
    </ul>
    <ul class="nav navbar-nav navbar-right">
      <li>
        <form
          action="/search?source=hp"
          method="post"
          id="search-form"
          class="form-inline"
        >
          <div class="form-group">
            <select name="cat" class="form-control" id="cat">
              <option value="movie">Movie Title</option>
              <option value="person">Actor</option>
            </select>
          </div>

          <input
            type="text"
            id="movie"
            placeholder="Search"
            name="movieSearch"
          />

          <input type="submit" class="btn btn-primary" />
        </form>
      </li>
    </ul>
  </div>
</nav>
```

---

- In views folder create single-movie.ejs, copy & paste template from resource

```html
<% include head %>
</head>
<body>
	<% include navbar %>
	<div class="container">
		<div class="row">
			<div class="col-sm-8 col-sm-offset-2 text-center">
				<h1 class="single-movie-title">
					<%= parsedData.title %>
				</h1>

				<h3 class="single-movie-title">
					<%= parsedData.tagline %>
				</h3>


				<a href="<%= parsedData.homepage %>"><img src="<%= imageBaseUrl+parsedData.poster_path %>" /></a>

				<p class="overview-header">Movie Synopsis: <span class="single-movie-overview">
					<%= parsedData.overview %>
				</span></p>
			</div>
		</div>
	</div>

<!-- Button trigger modal -->
<div class="col-sm-12 text-center">
	<button type="button" class="btn btn-primary btn-lg" data-toggle="modal" data-target="#myModal">
		More Details
	</button>
</div>

<!-- Modal -->
<div class="modal fade" id="myModal" tabindex="-1" role="dialog" aria-labelledby="myModalLabel">
  <div class="modal-dialog" role="document">
    <div class="modal-content">
      <div class="modal-header">
        <button type="button" class="close" data-dismiss="modal" aria-label="Close"><span aria-hidden="true">&times;</span></button>
        <h4 class="modal-title" id="myModalLabel">Movie Information</h4>
      </div>
      <div class="modal-body">
				<a href="https://www.imdb.com/title/<%= parsedData.imdb_id %>" target="_blank">IMDB link</a>
				<p><%= parsedData.budget %></p>
				<p><%= parsedData.revenue %></p>
				<p><%= parsedData.release_date%></p>
				<ul>
					<% parsedData.production_companies.forEach((company)=>{ %>
						<li><%= company.name %></li>
					<% }) %>
				</ul>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-default" data-dismiss="modal">Close</button>
        <button type="button" class="btn btn-primary">Save changes</button>
      </div>
    </div>
  </div>
</div>

</body>
</html>
```

---

- Rob way to organize tab: app | index.js i.e route | index.ejs | navbar.ejs | head.ejs
- localhost "http://localhost:3000/"

<br>

### 38. Adding the request module<a id="38"></a>

<br>

### 39. Putting the data in the template<a id="39"></a>

<br>

### 40. Adding the single-movie view<a id="40"></a>

<br>

### 41. Adding the search feature<a id="41"></a>

2. How and where to read api config<br>

- [apiKey ](https://www.themoviedb.org/) = "1fb720b97cc13e580c2c35e1138f90f8";
- apiBaseUrl = "http://api.themoviedb.org/3";
- [nowPlayingUrl ](https://developers.themoviedb.org/3/movies/get-now-playing) = `${apiBaseUrl}/most_popular?api_key=${apiKey}`;
- [imageBaseUrl](https://developers.themoviedb.org/3/configuration/get-api-configuration) = "http://image.tmdb.org/t/p/w300";
  <br>
  <br>

# Adding the request module

3. How to use [request module ](https://www.npmjs.com/package/request) ?
   <br>
   <br>

4. request.get takes 2 args:

- 1. it takes the URL to http "get"
- 2. the callback to run when the http response is back. 3 args:

  - 1. error (if any)
  - 2. http response
  - 3.  json/data the server sent back

            request.get( nowPlayingUrl, ( error, response, movieData ) => {}

        <br>
        <br>

5.  How to convert received http string message into JSON schema by [JSON.parse()](https://www.w3schools.com/js/js_json_parse.asp)

```
  const parsedData = JSON.parse(movieData);
```

    <br>
    <br>

# Putting data into template

6. How to read json schema object on browser-localhost to accessing object and use it like Rob did, instead on terminal

- video 39, time 09:00

```
  const parsedData = JSON.parse(movieData);
  // send the json to browser for
  res.json(parsedData)
```

  <br>
  <br>

7. How to make autimatically availabe the imageBaseUrl in all path in router

- we do it by using router.use() middleware, and then we add it to res.locals

```
  // Make available this imageBaseUrl to all paths
  router.use((req, res, next) => {
    // add imageBaseUrl to res.local so it will available in all path
    res.locals.imageBaseUrl = imageBaseUrl;
    next();
  });

```

- [My Space](https://myspace.com/discover/featured)
- [Wikipedia](https://en.wikipedia.org/wiki/Express.js)
  <br>
  <img src="notes/4%20server%20side%20rendering.png" width="700">
  <img src="notes/6%20my%20space.png" width="700">
  <br>
  <br>

# Notice

- Include head means, go and fetch this partial, it'll be just like taking this copying and pasting it right here in place of include head ejs -like Rob done it while explaining (video no 37, time-8:15)

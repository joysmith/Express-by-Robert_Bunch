#### 42. [Project Overview and Setup](#42)

#### 43. [Project structure and routes](#43)

#### 44. [First route and middleware](#44)

#### 45. [Movie Routes and some header work](#45)

#### 46. [Movie Routes and some header work - Continued](#46)

#### 47. [Search Routes with router.use()](#47)

---

<br>

### 42. Project Overview and Setup<a id='42'></a>

- ref. [TMDB api](https://developer.themoviedb.org/reference/movie-details)
- Starter [resource](https://github.com/robertbunch/justExpress/tree/master/starterFiles/apiProject2)

---

- Project setup

```sh
express movieApi
cd movieApi
npm install
npm i --save helmet
nodemon
```

- localhost "http://localhost:3000"

---

- In app.js import helmet and setup as middleware

```js
var createError = require("http-errors");
var express = require("express");
var path = require("path");
var cookieParser = require("cookie-parser");
var logger = require("morgan");
// import helmet
const helmet = require("helmet");

var indexRouter = require("./routes/index");
var usersRouter = require("./routes/users");

var app = express();
// setup helmet middleware
app.use(helmet());

// view engine setup
app.set("views", path.join(__dirname, "views"));
app.set("view engine", "jade");

app.use(logger("dev"));
app.use(express.json());
app.use(express.urlencoded({ extended: false }));
app.use(cookieParser());
app.use(express.static(path.join(__dirname, "public")));

app.use("/", indexRouter);
app.use("/users", usersRouter);

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

- create data-folder in rootlevel, and init create movieDetails.js file

  - copy and paste json from starter to movieDetails.js

  - Starter [resource](https://github.com/robertbunch/justExpress/tree/master/starterFiles/apiProject2)

- In data-folder create movie.js file

  - copy and paste json from starter to movie.js

  - Starter [resource](https://github.com/robertbunch/justExpress/tree/master/starterFiles/apiProject2)

- In data-folder create people.js file

  - copy and paste json from starter to people.js

  - Starter [resource](https://github.com/robertbunch/justExpress/tree/master/starterFiles/apiProject2)

  <br>

### 43. Project structure and routes<a id='43'></a>

- Delete users.js from route-folder
- In app.js remove, users route import & and route setup

```js
var createError = require("http-errors");
var express = require("express");
var path = require("path");
var cookieParser = require("cookie-parser");
var logger = require("morgan");
const helmet = require("helmet");

var indexRouter = require("./routes/index");
// var usersRouter = require("./routes/users");  ---remove

var app = express();
app.use(helmet());

app.set("views", path.join(__dirname, "views"));
app.set("view engine", "jade");

app.use(logger("dev"));
app.use(express.json());
app.use(express.urlencoded({ extended: false }));
app.use(cookieParser());
app.use(express.static(path.join(__dirname, "public")));

app.use("/", indexRouter);
// app.use("/users", usersRouter); ---remove

app.use(function (req, res, next) {
  next(createError(404));
});

app.use(function (err, req, res, next) {
  res.locals.message = err.message;
  res.locals.error = req.app.get("env") === "development" ? err : {};

  res.status(err.status || 500);
  res.render("error");
});

module.exports = app;
```

---

- In routes-folder create: movie.js, search.js
- In routes/movie.js

```js
var express = require("express");
var router = express.Router();

// GET movie page
//      /movie/
router.get("/", (req, res, next) => {
  res.render("index", { title: "Express" });
});

module.exports = router;
```

---

- In routes/search.js

```js
var express = require("express");
var router = express.Router();

// GET search page
//      /search/
router.get("/", (req, res, next) => {
  res.render("index", { title: "Express" });
});

module.exports = router;
```

---

- In app.js import routes and set them up as middleware

```js
var createError = require("http-errors");
var express = require("express");
var path = require("path");
var cookieParser = require("cookie-parser");
var logger = require("morgan");

const helmet = require("helmet");

/* IMPORT ROUTES */
// /now_playing
var indexRouter = require("./routes/index");
// /movies/...
const movieRouter = require("./routes/movie");
// /search/...
const searchRouter = require("./routes/search");

var app = express();
app.use(helmet());

app.set("views", path.join(__dirname, "views"));
app.set("view engine", "jade");

app.use(logger("dev"));
app.use(express.json());
app.use(express.urlencoded({ extended: false }));
app.use(cookieParser());
app.use(express.static(path.join(__dirname, "public")));

/* SETUP ROUTES MIDDLEWARE */
app.use("/", indexRouter);
app.use("/movie", movieRouter);
app.use("/search", searchRouter);

app.use(function (req, res, next) {
  next(createError(404));
});

app.use(function (err, req, res, next) {
  res.locals.message = err.message;
  res.locals.error = req.app.get("env") === "development" ? err : {};

  res.status(err.status || 500);
  res.render("error");
});

module.exports = app;
```

- Go to localhost "http://localhost:3000/search"

<br>

### 44. First route and middleware<a id='44'></a>

- In routes/index.js, filtering most popular movie from db

```js
var express = require("express");
var router = express.Router();

const movies = require("../data/movies");

/* GET home page. */
router.get("/", function (req, res, next) {
  res.render("index", { title: "Express" });
});

router.get("/most_popular", function (req, res, next) {
  // filter is a prototye method on all array that gives filtered rerults in form of array
  // it takes callback as an argument
  const results = movies.filter((movie) => {
    return movie.most_popular;
  });

  res.json(results);
});

module.exports = router;
```

- Go to localhost "http://localhost:3000/most_popular"

---

- In routes/index.js, adding api_key feature to show most popular movie

```js
var express = require("express");
var router = express.Router();

const movies = require("../data/movies");

/* GET home page. */
router.get("/", function (req, res, next) {
  res.render("index", { title: "Express" });
});

router.get("/most_popular", function (req, res, next) {
  // condition:shoud have api key with value 123456789
  if (req.query.api_key != 123456789) {
    res.json("Invalid API key");
  } else {
    // filter most popular
    const results = movies.filter((movie) => {
      return movie.most_popular;
    });
    res.json(results);
  }
});

module.exports = router;
```

- Go to localhost "http://localhost:3000/most_popular?api_key=123456wrong"
- Go to localhost "http://localhost:3000/most_popular?api_key=123456789"

---

- In routes/index.js, adding pagination feature

```js
var express = require("express");
var router = express.Router();

const movies = require("../data/movies");

/* GET home page. */
router.get("/", function (req, res, next) {
  res.render("index", { title: "Express" });
});

router.get("/most_popular", function (req, res, next) {
  let page = req.query.page;
  // condition: page is not provided in query string
  if (page === undefined) {
    // set default page 1
    page = 1;
  }

  // condition:shoud have api key with value 123456789
  if (req.query.api_key != 123456789) {
    res.json("Invalid API key");
  } else {
    // filter most popular
    let results = movies.filter((movie) => {
      return movie.most_popular;
    });

    // only show 20 item per page
    const indexToStart = (page - 1) * 20;
    results = results.slice(indexToStart, indexToStart + 19);

    res.json(results);
  }
});

module.exports = router;
```

- Go to localhost "http://localhost:3000/most_popular?api_key=123456789"

---

- In routes/index.js, adding pagination feature sending response in form of object

```js
var express = require("express");
var router = express.Router();

const movies = require("../data/movies");

/* GET home page. */
router.get("/", function (req, res, next) {
  res.render("index", { title: "Express" });
});

router.get("/most_popular", function (req, res, next) {
  let page = req.query.page;
  if (page === undefined) {
    page = 1;
  }

  // condition:shoud have api key with value 123456789
  if (req.query.api_key != 123456789) {
    res.json("Invalid API key");
  } else {
    // filter most popular
    let results = movies.filter((movie) => {
      return movie.most_popular;
    });

    // only show 20 item per page
    const indexToStart = (page - 1) * 20;
    results = results.slice(indexToStart, indexToStart + 19);

    res.json({ page, results });
  }
});

module.exports = router;
```

- Go to localhost "http://localhost:3000/most_popular?api_key=123456789"

<br>

### 45. Movie Routes and some header work<a id='45'></a>

<br>

### 46. Movie Routes and some header work - Continued<a id='46'></a>

<br>

### 47. Search Routes with router.use()<a id='47'></a>

<br>

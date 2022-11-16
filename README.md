# How to create express server manually

1. Create project folder on Desktop
2. Open this folder with VS code editor
3. Create a file server.js
4. Initialize with with default options from terminal

```
    npm init -y
```

5. Install express, body-parser, helmet, ejs cookie-parser, request modules from terminal

```
   npm install express helmet ejs request cookie-parser --save
```

6. (optional) Install nodemon from terminal
7. Copy the skelton code in server.js from github or expressjs

```
    const express = require("express");
    const app = express();
    const port = 3000;

    app.get("/", (req, res) => {
    res.send("Hello World!");
    });

    app.listen(port, () => {
    console.log(`Example app listening on port ${port}`);
    });
```

8. Run the server with " nodemon server.js" from terminal
9. Use Chrome to make connection with server
   <br>
   <br>
   <br>
   <br>

# How to create express server scaffold with express generator

1. Create project folder on Desktop
2. Open this folder with VS code editor
3. Install express generator tool from terminal

```
	npm install -g express-generator
```

4. Create express server with default ejs view engine

```
	express projectname --view=ejs
```

4. Create simple express server without any view engine

```
	express projectname
```

5.  Change directory to projectname from terminal

6.  Then run cmd from terminal to install dependencies

```
    npm install
```

7. (Optional) Install other modules

```
   npm install helmet request  --save
```

8. Place the module and use them in layout in following order

```

    var createError = require('http-errors');
    var express = require('express');
    var app = express();                //  1

    const helmet = require('helmet')    //  2
    app.use(helmet());                  //  3

    var path = require('path');
    var cookieParser = require('cookie-parser');
    var logger = require('morgan');

    var indexRouter = require('./routes/index');
    var usersRouter = require('./routes/users');

    // view engine setup
    app.set('views', path.join(__dirname, 'views'));
    app.set('view engine', 'jade');

    app.use(logger('dev'));
    app.use(express.json());
    app.use(express.urlencoded({ extended: false }));
    app.use(cookieParser());
    app.use(express.static(path.join(__dirname, 'public')));

    app.use('/', indexRouter);
    app.use('/users', usersRouter);

    // catch 404 and forward to error handler
    app.use(function(req, res, next) {
    next(createError(404));
    });

    // error handler
    app.use(function(err, req, res, next) {
    // set locals, only providing error in development
    res.locals.message = err.message;
    res.locals.error = req.app.get('env') === 'development' ? err : {};

    // render the error page
    res.status(err.status || 500);
    res.render('error');
    });

    module.exports = app;


```

```

```

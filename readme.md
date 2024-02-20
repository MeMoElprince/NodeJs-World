# Welcome 
<hr>

## Hello NodeJs

<p><b> I've gone a little deep into backend development with NodeJs, Express and mongoDB, so this documentation will cover some of my experience and knowledge in the backend in general and specificly in NodeJs </b></p>

<hr>

## Refreshing the basics


<details>
<summary><b id='nodejs'>NodeJs</b></summary>

> Node.js is an open-source, cross-platform, back-end JavaScript runtime environment that runs on the V8 engine and executes JavaScript code outside a web browser.

> Modules are the building blocks of Node.js, they are reusable pieces of code that can be exported from one program and imported for use in another program.

```javascript
(
    function (exports, require, module, __filename, __dirname) {
        // Module code actually lives in here
        
        
    }
);

```

> Node.js has a set of built-in modules which you can use without any further installation.

#### Table of Contents
- [File System](#file-system) 
- [HTTP](#http)
- [Path](#path)
- [Operating System](#os)
- [Events](#events)

> <p id='file-system'>File System Module</p>
```javascript
const fs = require('fs');

fs.readFile('file.txt', 'utf8', (err, data) => {
    if (err) throw err;
    console.log(data);
});

fs.writeFile('file.txt', 'Hello NodeJs', (err) => {
    if (err) throw err;
    console.log('The file has been saved!');
});

fs.appendFile('file.txt', 'Hello NodeJs', (err) => {
    if (err) throw err;
    console.log('The file has been saved!');
});

fs.unlink('file.txt', (err) => {
    if (err) throw err;
    console.log('The file has been deleted!');
});

fs.rename('file.txt', 'newfile.txt', (err) => {
    if (err) throw err;
    console.log('The file has been renamed!');
});
```

> <p id='http'>HTTP Module</p>
```javascript
const http = require('http');

http.createServer((req, res) => {
    res.writeHead(200, {'Content-Type': 'text/html'});
    res.write('Hello World!');
    res.end();
}).listen(8080);


// URL Module
const url = require('url');

const adr = 'http://localhost:8080/default.htm?year=2017&month=february';
const q = url.parse(adr, true);
```

> <p id='path'>Path Module</p>
```javascript
const path = require('path');

path.parse(__filename);
path.join(__dirname, 'example.txt'); 
path.resolve('example.txt'); 
```

> <p id='os'>Operating System Module</p>
```javascript
const os = require('os');

os.cpus(); // Returns an array of objects containing information about each CPU/core installed
os.freemem(); // Returns the amount of free system memory in bytes
os.totalmem(); // Returns the total amount of system memory in bytes
os.homedir(); // Returns the home directory of the current user
os.hostname(); // Returns the hostname of the operating system
os.networkInterfaces(); // Returns an object containing information about the network interfaces of the machine
os.platform();  // Returns the operating system platform
os.release(); // Returns the operating system release
os.tmpdir(); // Returns the operating system's default directory for temporary files
os.type(); // Returns the operating system name
```
    
> <p id='events'>Events Module</p>
```javascript
const events = require('events');

const eventEmitter = new events.EventEmitter();

eventEmitter.on('scream', () => {
    console.log('I hear a scream!');
});

eventEmitter.emit('scream');
```


</details>

<details>
<summary><b>Express</b></summary>

#### Table of Contents
- [Basic Express Server](#basic-express-server) 
- [Express Middleware](#express-middleware)
- [Express Router](#express-router)
- [Express Static Files](#express-static-files)
- [Express Template Engine](#express-template-engine)
- [Express Error Handler](#express-error-handler)
  
> <p id='basic-express-server'>Basic Express Server</p>
```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
    res.send('Hello World!');
});

app.listen(3000, () => {
    console.log('Server is running on port 3000');
});
```

> <p id='express-middleware'>Express Middleware </p>
```javascript
const express = require('express');
const app = express();

app.use((req, res, next) => {
    console.log('Time:', Date.now());
    next();
});

app.get('/', (req, res) => {
    res.send('Hello World!');
});

app.listen(3000, () => {
    console.log('Server is running on port 3000');
});
```

> <p id='express-router'>Express Router</p>
```javascript
const express = require('express');
const app = express();
const router = express.Router();

router.use((req, res, next) => {
    console.log('Time:', Date.now());
    next();
});

router.get('/', (req, res) => {
    res.send('Hello World!');
});

app.use('/', router);

app.listen(3000, () => {
    console.log('Server is running on port 3000');
});
```

> <p id='express-static-files'>Express Static Files</p>
```javascript
const express = require('express');
const app = express();

app.use(express.static('public'));

app.listen(3000, () => {
    console.log('Server is running on port 3000');
});
```

> <p id='express-template-engine'>Express Template Engine</p>
```javascript
const express = require('express');
const app = express();

app.set('view engine', 'pug');
app.set('views', './views');

app.get('/', (req, res) => {
    res.render('index', { title: 'Hey', message: 'Hello there!' });
});

app.listen(3000, () => {
    console.log('Server is running on port 3000');
});
```

> <p id='express-error-handler'>Express Error Handling</p>
```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
    throw new Error('BROKEN');
});

app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).send('Something broke!');
});

app.listen(3000, () => {
    console.log('Server is running on port 3000');
});
```
</details>

<details>
<summary><b>MongoDB</b></summary>

> MongoDB is a cross-platform document-oriented database program. Classified as a NoSQL database program, MongoDB uses JSON-like documents with optional schemas.

```javascript
const MongoClient = require('mongodb').MongoClient;
const url = 'mongodb://localhost:27017/mydb';

MongoClient.connect(url, (err, db) => {
    if (err) throw err;
    console.log('Database created!');
    db.close();
});

MongoClient.connect(url, (err, db) => {
    if (err) throw err;
    const dbo = db.db('mydb');
    dbo.createCollection('customers', (err, res) => {
        if (err) throw err;
        console.log('Collection created!');
        db.close();
    });
});

MongoClient.connect(url, (err, db) => {
    if (err) throw err;
    const dbo = db.db('mydb');
    const myobj = { name: 'Company Inc', address: 'Highway 37' };
    dbo.collection('customers').insertOne(myobj, (err, res) => {
        if (err) throw err;
        console.log('1 document inserted');
        db.close();
    });
});
```
</details>

<details>
<summary><b>Mongoose</b></summary>

> Mongoose is a MongoDB object modeling tool designed to work in an asynchronous environment. Mongoose supports both promises and callbacks.

#### Table of Contents
- [Mongoose Schema](#mongoose-schema) 
- [Mongoose Query](#mongoose-query)
- [Mongoose Operations](#mongoose-operations)

> Mongoose Schema
```javascript
const mongoose = require('mongoose');
mongoose.connect('mongodb://localhost/test', {useNewUrlParser: true, useUnifiedTopology: true});

const Schema = mongoose.Schema;
const ObjectId = Schema.ObjectId;

const BlogPost = new Schema({

    feild1: {
        type: String,
        required: true,
        unique: true,
        lowercase: true,
        trim: true,
        match: /[a-z]/,
    },
    feild2: {
        type: String,
        required: true,
        enum: ['value1', 'value2', 'value3'],
        default: 'value1',
        validate: (value) => {
            return value.length > 0;
        },
        get: (value) => {
            return value.toUpperCase();
        }
    },
    feild3: {
        type: ObjectId,
        ref: 'Model'
    },
    feild4: {
        type: Date,
        default: Date.now
    }
},
{
    //  When set toObject and toJSON, virtuals are enabled by default
    // Working with populate for example
    toObject: { virtuals: true },
    toJSON: { virtuals: true }
});

const Model = mongoose.model('Model', BlogPost);
```

> <p id='mongoose-schema'>Mongoose Middleware</p>
```javascript
const mongoose = require('mongoose');
mongoose.connect('mongodb://localhost/test', {useNewUrlParser: true, useUnifiedTopology: true});

const Schema = mongoose.Schema;

const BlogPost = new Schema({
    title: String,
    body: String
});

BlogPost.pre('save', function(next) {
    // do something
    next();
});

BlogPost.post('save', function(doc) {
    // do something
});

const Model = mongoose.model('Model', BlogPost);
```

> <p id='mongoose-query'>Mongoose Query</p>
```javascript
const mongoose = require('mongoose');
mongoose.connect('mongodb://localhost/test', {useNewUrlParser: true, useUnifiedTopology: true});

const Schema = mongoose.Schema;

const BlogPost = new Schema({
    title: String,
    body: String
});

const Model = mongoose.model('Model', BlogPost);

Model.find({ title: 'title' }, (err, docs) => {
    // do something
});

Model.findOne({ title: 'title' }, (err, doc) => {
    // do something
});

Model.findById('id', (err, doc) => {
    // do something
});

Model.findByIdAndRemove('id', (err, doc) => {
    // do something
});

Model.findByIdAndDelete('id', (err, doc) => {
    // do something
});

Model.findByIdAndUpdate('id', { title: 'title' }, (err, doc) => {
    // do something
});

Model.findOneAndRemove({ title: 'title' }, (err, doc) => {
    // do something
});

Model.findOneAndDelete({ title: 'title' }, (err, doc) => {
    // do something
});

Model.findOneAndUpdate({ title: 'title' }, { title: 'title' }, (err, doc) => {
    // do something
});
```

> <p id='mongoose-operations'>Mongoose Operations</p>
```javascript
const mongoose = require('mongoose');
mongoose.connect('mongodb://localhost/test', {useNewUrlParser: true, useUnifiedTopology: true});

const Schema = mongoose.Schema;

const BlogPost = new Schema({
    title: String,
    body: String
});

const Model = mongoose.model('Model', BlogPost);

Model.create({ title: 'title', body: 'body' }, (err, doc) => {
    // do something
});

Model.insertMany([{ title: 'title', body: 'body' }], (err, docs) => {
    // do something
});

Model.update({ title: 'title' }, { title: 'title' }, (err, raw) => {
    // do something
});

Model.updateOne({ title: 'title' }, { title: 'title' }, (err, raw) => {
    // do something
});

Model.updateMany({ title: 'title' }, { title: 'title' }, (err, raw) => {
    // do something
});

Model.deleteOne({ title: 'title' }, (err) => {
    // do something
});

Model.deleteMany({ title: 'title' }, (err) => {
    // do something
});
```
</details>

<details>
<summary><b>Authentication</b></summary>

> Authentication is the process of verifying the identity of a user. It is the mechanism of associating an incoming request with a set of identifying credentials, such as the user the request came from, or the token that it was signed with.

#### Table of Contents
- [JWT](#jwt)
- [Authentication](#authentication)
  
> <p id='jwt'>JWT</p>
```javascript
const jwt = require('jsonwebtoken');

const token
    = jwt.sign
    (
        { 
            data: 'foobar' 
        },
        'secret',
        { 
            expiresIn: '1h' 
        }
    );

const decoded
    = jwt.verify
    (
        token,
        'secret'
    );
```

> <p id='authentication'>Authentication</p>
```javascript
```
</details>

<details>
<summary><b>Authorization</b></summary>

> Authorization is the process of giving someone permission to do or have something. In multi-user computer systems, a system administrator defines for the system which users are allowed access to the system and what privileges of use (such as access to which file directories, hours of access, amount of allocated storage space, and so forth).


</details>

<details>
<summary><b>Error Handling</b></summary>

> Error handling refers to the anticipation, detection, and resolution of programming, application, and communications errors. Specialized programs, called error handlers, are available for some applications.



</details>

<details>
<summary><b>Security</b></summary>

> Security is the degree of resistance to, or protection from, harm. It applies to any vulnerable and valuable asset, such as a person, dwelling, community, item, nation, or organization.
> As noted in the [Authentication](#authentication) section, JWT is a good way to secure your application.
> Also, you can use Helmet to secure your application.

```javascript
const helmet = require('helmet');
app.use(helmet());
```

</details>

<details>
<summary><b>Performance</b></summary>

> Performance is the extent to which a system, device, or component is able to do work and yield a result within a given time frame.
> You can use compression to improve the performance of your application.

```javascript
const compression = require('compression');
app.use(compression());
```
</details>

<details>
<summary><b>Deploying</b></summary>

</details>

<hr>

## Practical Examples

<details>
<summary><b>Advanced Mongoose</b></summary>

</details>

<details>
<summary><b>Geospatial Queries</b></summary>

</details>

<details>
<summary><b>Image Proccessing & File Uploads</b></summary>

</details>

<details>
<summary><b>Map</b></summary>

</details>

<details>
<summary><b>Email Template</b></summary>

</details>

<details>
<summary><b>Cookiees</b></summary>

</details>

<details>
<summary><b>Payments With Stripe</b></summary>

</details>

<hr>

## Notes & Tips

> coming soon ...

<hr>

#### This Repo is still under development, so stay tuned for more updates and improvements.





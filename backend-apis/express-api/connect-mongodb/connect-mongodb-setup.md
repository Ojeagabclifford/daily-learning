
📂 Setup: How to connect to mongoDb

This is the process I use to connect to my MongoDb in my node project first you need two files if you want to follow MVC pettan .
First you need a model folder and inside the model fother you need a file you can name it the way you like but will called it db.js this file contain the code that need to be excuted for the conncet to be made.
/////
Secound you need a server.js file which is already in your root folder where your app start from,
why we need this is becuase that is the place your app start from so you need to start the db connection imdiatly your app start so it can intialize the funtion you will import from the db.js which i will show you in the code later.


The Code

TO installl the packge into your node project you need 
this code
npm install mongoose dotenv
one to install mongoose and the other to install dotenv i will show later how i use it.


in your .env file this string need to be there and i will show you what it will be used for
MONGODB_URI=mongodb+srv://cliffordlearning123:password@cluster0.pbtu99q.mongodb.net/users

In your model/db.js you will have this code.
This code create the connect to mongodb.

const dotenv = require('dotenv');
this is the code to import the dotenv package you install into your db.js file and store it into a variable call called dotenv which you will use later.
dotenv.config();

const MongoClient = require('mongodb').MongoClient;
this import the mongo clint into he files and the .Mongoclint tells mongodb taht you will be using mongoclint tool because mongodb clint has many tools.

let _db;
const initDb = asycn ()=> {
    try{

   
// in this top code we are using an exprestion function  
// with a variable name initDb it has a call back function that act like Async/Await. that return a sign after the database has worked.
 
  if (_db) {
    //This check if the data base if already initialized
    console.warn('Db is already initialized!');
  // If true return the database
    return _db
  }

  const client = await MongoClient.connect(process.env.MONGODB_URI)
  
  _db = client.db(process.env.MONGODB_DB_NAME);
    
    return _db
    }
    catch(err){
        throw err
    }
};

const getDb = () => {
  if (!_db) {
    throw Error('Db not initialized');
  }
  return _db;
};

module.exports = {
  initDb,
  getDb,
};


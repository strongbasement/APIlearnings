# APIlearnings 


# To know about ApI we are going to use joke api Api is nothing but information or services provided by an organization

## let create a app.js to fetch from jokeapi

### step 1:create an app.js and index.html in one folder

### step 2:create a form in index.js to sumbit the data for type of joke

``` html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>let me make you laugh</h1>
    <form action="/" method="post">
        <input type="text" name="joketype" placehoder="enter the joketype">
        <input type="submit">
    </form>
</body>
</html>

```

### step 3:After finishing html part we are going to get or fetch data from joke api through their api address

### note:  Before going through this concept you need to know about or refresh the concept of [express-listen](https://github.com/strongbasement/mylearnings-nodejs-express/blob/main/running%20server%20using%20express/express-listen.md), [express-get](https://github.com/strongbasement/mylearnings-nodejs-express/blob/main/running%20server%20using%20express/express-get.md),[express-post](https://github.com/strongbasement/mylearnings-nodejs-express/blob/main/running%20server%20using%20express/express-post.md).

### step 4: from getting data from joke api we can use https module from node-js


``` js
const https=require('https');
```

### step 5: watch code mentioned below 

``` js
app.post('/',function(req,res) //this is the post method called when form submit is clicked req is parameter to request anything,by res we can response to users

{
   var joke;  
var types=req.body.joketype; /*storing input type text field value in a variable called types . req is request to body ie form.html;body is bodyparser function;joketype is input type name mentioned while in form creation */ 
var url='https://v2.jokeapi.dev/joke/'+types;//we are requesting data from this url 
https.get(url,(response)=>//https method to get data from url,response is function parameter to detect the response status
{
    console.log(response.statusCode);//we are checking the response is ok if it gives 200 its ok which means content delivered successfully
    response.on("data",(data)=> //this lines tell how to respond on reciving data from jokeapi
    {
        joke=JSON.parse(data).joke;//storing data provided by joke api inside global variable joke;json.parse convert json data into normal text,json.stringify is opposite of it
        
    res.send(joke); //sending joke as response
    }
    );
});
});
```

# Final code

``` js

const express=require('express');
const app=express();
const bodyparser=require('body-parser');
const https=require('https');
app.use(bodyparser.urlencoded({extended:true}));

app.listen(3000,()=>
{
  console.log('running on 3000');  
}


);

app.get('/',function(req,res)

{
    res.sendFile(__dirname+'/index.html');
}

);
app.post('/',function(req,res)

{
    var joke;  
var types=req.body.joketype; /*storing input type name field value in a variable called. req is request to body ie form.html;body is bodyparser function;name1 is input type name mentioned while in form creation */ 
var url='https://v2.jokeapi.dev/joke/'+types;
https.get(url,(response)=>
{
    console.log(response.statusCode);
    response.on("data",(data)=>
    {
        
        joke=JSON.parse(data).joke;
        if(joke==null)
        {
                   joke=JSON.parse(data).setup;
 
        }
    res.send(joke);
    }
    );
    
});

});

```
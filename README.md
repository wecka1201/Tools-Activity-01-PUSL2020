const express = require('express');
const app = express();

app.use(express.urlencoded({ extended: true }));

let storedName = ""; 

const commonCSS = `
    <style>
        body {
            background-color: #0d0d1a;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            color: white;
        }
        .card {
            background-color: #1a1a33;
            padding: 50px 40px;
            border-radius: 20px;
            text-align: center;
            width: 350px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.5);
        }
        h2 {
            color: #a37bff; 
            font-size: 36px;
            margin-top: 0;
            margin-bottom: 10px;
            font-weight: 600;
        }
        p {
            color: #9395ad;
            font-size: 15px;
            margin-bottom: 30px;
        }
        input {
            width: 100%;
            padding: 15px;
            margin-bottom: 25px;
            background-color: #111122;
            border: 1px solid #2a2a45;
            border-radius: 10px;
            color: white;
            box-sizing: border-box;
            font-size: 15px;
        }
        input:focus {
            outline: none;
            border-color: #645bff;
        }
        button {
            width: 100%;
            padding: 15px;
            background-color: #645bff;
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: 0.3s;
        }
        button:hover {
            background-color: #5247e6;
        }
        a {
            color: #9395ad;
            text-decoration: none;
            font-size: 15px;
            display: inline-block;
            margin-top: 20px;
        }
        a:hover {
            color: white;
        }
    </style>
`;

app.get('/', (req, res) => {
    res.send(`
        <!DOCTYPE html>
        <html>
        <head>
            <title>Welcome</title>
            ${commonCSS}
        </head>
        <body>
            <div class="card">
                <h2>Welcome</h2>
                <p>Please enter your name to receive a greeting.</p>
                <form action="/submit" method="POST">
                    <input type="text" name="userName" placeholder="Enter your name" required>
                    <button type="submit">Get Greeting</button>
                </form>
            </div>
        </body>
        </html>
    `);
});

app.post('/submit', (req, res) => {
    storedName = req.body.userName; 
    res.redirect('/greeting'); 
});

app.get('/greeting', (req, res) => {
    res.send(`
        <!DOCTYPE html>
        <html>
        <head>
            <title>Greeting</title>
            ${commonCSS}
        </head>
        <body>
            <div class="card">
                <h2>Hello, ${storedName}!</h2>
                <a href="/">Go Back</a>
            </div>
        </body>
        </html>
    `);
});

const PORT = 3000;
app.listen(PORT, () => {
    console.log(`Server running at http://localhost:${PORT}`);
});

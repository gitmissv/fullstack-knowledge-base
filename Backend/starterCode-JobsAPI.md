#Start New Project#

    npm init -y
    git init

    // Install dependencies
    npm i mongoose express dotenv

    // Install devDependencies
    npm i -D nodemon

    Change package.json "scripts"

# Add Files and Folders

    .env
    .gitignore (add node_modules & .env)
    app.js

    controllers
        auth.controller.js

    lib
        constants.lib.js
        mongoose.lib.js
        response.lib.js

    middleware
        auth.middleware.js

    models
        user.model.js

    routes
        auth.route.js

# STARTER CODE

app.js

    // * IMPORTS
    require("dotenv").config();
    require("express-async-errors");

    const express = require("express");
    const cors = require("cors");
    const app = express();

    const connectToMongo = require("./lib/mongoose");
    const { PORT, SERVER_URL } = require("./lib/constants");

    // * MIDDLEWARES
    app.use(cors()); // CORS
    app.use(express.json()); // Body Parser

    // * ROUTES
    app.use("/api/v1/auth", require("./routes/auth.routes"));

    // * START SERVER & DB
    (async () => {
        try {
            // TODO Start Database

            // Start Server
            app.listen(PORT, () => console.log(`Server Listening: ${SERVER_URL}`));
        } catch (err) {
            console.log("ERROR:", err);
        }
    })();

## CONTROLLERS

auth.controller.js

    // * IMPORTS
    const { successfulRes, unsuccessfulRes } = require("../lib/response");

    // * CONTROLLERS
    // TODO Register a User - POST: /api/v1/auth/register
    async function registerUser(req, res) {}

    // TODO: Login a User - POST: /api/v1/auth/login
    async function loginUser(req, res) {}

    // * EXPORTS
    module.exports = {
        registerUser,
        loginUser,
    };

## LIB

constants.lib.js

    // * CONSTANTS
    const PORT = 5050;
    const SERVER_URL = `http://localhost:${PORT}`;

    // * EXPORTS
    module.exports = {
        PORT,
        SERVER_URL,
    };

mongoose.lib.js

    // * IMPORTS
    const mongoose = require("mongoose");

    // * METHODS
    function connectToMongo(dbConnectionString) {
        try {
            const dbConnection = mongoose.connect(dbConnectionString);

            const MONGO_DB_NAME = dbConnectionString
                .split("mongodb.net/")[1]
                .split("?")[0];

            console.log(`Connected to MongoDB Database (${MONGO_DB_NAME})`);

          return dbConnection;
        } catch (err) {
            console.log("ERROR CONNECTING TO DB:", err);
        }
    }

    // * EXPORTS
    module.exports = connectToMongo;

response.lib.js

    // * IMPORTS

    // * METHODS
    // SUCCCESS RESPONSE
    function successfulRes({ res, status = 200, data = {} }) {
        return res.status(status).json({
            success: true,
            error: null,
            data,
        });
    }

    // ERROR RESPONSE
    function unsuccessfulRes({
        res,
        status = 400,
        message = "Uh oh! Something went wrong.",
     }) {
        return res.status(status).json({
            success: false,
            error: {
            status,
            message,
        },
        data: null,
        });
    }

    // * EXPORTS
    module.exports = {
        successfulRes,
        unsuccessfulRes,
    };

## MIDDLEWARE

auth.middleware.js

    // * IMPORTS

    // * MIDDLEWARE
    // TODO: Middleware to Grab & Check JWT from Auth Headers
    async function authMiddleware(req, res, next) {

    // Extract auth headers from request

    // Check for existance and bearer prefix

    // Seperate token from 'Bearer'

    try {
        // Verify the given token
        // Attach the username to the request
        // Next Middleware
    } catch (error) {
        // Verification Failed
    }
    }

    // * EXPORTS
    module.exports = authMiddleware;

## MODELS

user.model.js

    // * IMPORTS
    const { model, Schema } = require("mongoose");

    // * MODEL
    const UserSchema = new Schema({
        name: {
            type: String,
        },
        email: {
            type: String,
        },
        password: {
            type: String,
        },
    });

    // * METHODS
    // TODO Salt & Hash Password Before Save New User

    // * Create JWT Method

    // TODO: Compare Incoming Password w/ DB Password

    // * EXPORTS
    module.exports = model("User", UserSchema);

## ROUTES

auth.routes.js

    // * IMPORTS
    const router = require("express").Router();

    const { registerUser, loginUser } = require("../controllers/auth.controllers");

    // * ROUTES
    // TODO REGISTER (add route)

    // TODO LOGIN (add route)

    // * EXPORTS
    module.exports = router;

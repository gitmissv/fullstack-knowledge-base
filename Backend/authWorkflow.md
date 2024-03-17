a# Auth Workflow #

	-register user > send email
	-user verifies email > backend confirms account
	-user able to login > backend verifies user & pwd
	
	---success! || error!!

## Verify Token #

In *user.model.js* file – Add verificationToken (see bottom code):

	const UserSchema = new mongoose.Schema({
		name: {
			type: String,
			required: [true, "Please provide name"],
			minlength: 3,
			maxlength: 50,
		},

		email: {
			type: String,
			unique: true,
			required: [true, "Please provide email"],
			validate: {
				validator: validator.isEmail,
				message: "Please provide valid email",
			},
		},

		password: {
			type: String,
			required: [true, "Please provide password"],
			minlength: 6,
		},

		role: {
			type: String,
			enum: ["admin", "user"],
			default: "user",
		},

		verificationToken: String,
			isVerified: {
				type: Boolean,
				default: false,
			},

		verified: Date,
		});

In *auth.controller.js* file – Add verificationToken AND verifyEmail to user:

	const isFirstAccount = (await User.countDocuments({})) === 0;
	const role = isFirstAccount ? "admin" : "user";

	const verificationToken = crypto.randomBytes(40).toString("hex");

	const user = await User.create({
		name,
		email,
		password,
		role,
		verificationToken,
	});

// ! send verification token back only while testing in postman!

	res.status(StatusCodes.CREATED).json({
		msg: "Success! Please check your email to verifiy account",
		verificationToken: user.verificationToken,
		});
	};

// ** VERIFY EMAIL **

	const verifyEmail = async (req, res) => {
	const { verificationToken, email } = req.body;
		res.status(StatusCodes.OK).json({ verificationToken, email });
	};

**SEE ALSO CHANGES TO VERIF EMAIL AFTER TESTING COMPLETE**

In *auth.routes.js* file – Add verifyEmail:

	const express = require("express");
	const router = express.Router();

	const {
		register,
		login,
		logout,
		verifyEmail,
	} = require("../controllers/authController");

	router.post("/register", register);
	router.post("/login", login);
	router.get("/logout", logout);
	router.post("/verify-email", verifyEmail);

	module.exports = router;

** VERIFY EMAIL – AFTER TESTING COMPLETE**

in authController:

	// * VERIFY EMAIL
	const verifyEmail = async (req, res) => {
	const { verificationToken, email } = req.body;

	const user = await User.findOne({ email });

	if (!user) {
		throw new CustomError.UnauthenticatedError("Verification Failed!");
	}

	if (user.verificationToken !== verificationToken) {
		throw new CustomError.UnauthenticatedError("Verification Failed!");
	}

	(user.isVerified = true), (user.verified = Date.now());
	user.verificationToken = "";

	await user.save();

	res.status(StatusCodes.OK).json({ msg: "Email Verified" });
	};

## Send Email Setup #

Install Nodemailer:

	npm install nodemailer

create files in utils folder:

   - nodemailerConfig.js
   - sendEmail.js
   - sendResetPasswordEmail.js
   - sendVerificationEmail.js

## Crypto Library – Built in to Node #

Import library:

	const crypto = require(‘crypto’)

Add to your verification (login / register):

	const verificationToken = cypto.randomBytes( 40 ).toString(‘hex’):


# Refresh Tokens #

Expiration examples:

   OneDay:  
      const oneDay = 1000 * 60 * 60 * 24;
   
	5 Seconds:
      const fiveSeconds = 1000 * 5


*Access Tokens* = very short expiration

*Refresh Token* = time to allow user to get things done (15 min; 1 hour; 1 day; etc.)


## Token Model #

	const mongoose = require("mongoose");

	const TokenSchema = new mongoose.Schema({
		refreshToken: { type: String, required: true },
    	ip: { type: String, required: true },
    	userAgent: { type: String, required: true },
    	isValid: { type: Boolean, default: true },
    	user: {
      	type: mongoose.Types.ObjectId,
      	ref: "User",
      	required: true,
    	},
  	},
  	{ timestamps: true }
	);

	module.exports = mongoose.model("Token", TokenSchema);


In auth.controller; after user login is verified, add token data:

	if (!user.isVerified) {
   	throw new CustomError.UnauthenticatedError("Please verify your email");
  	}
  	const tokenUser = createTokenUser(user);

	// create refresh token
	let refreshToken = "";

	// check for existing token
	const existingToken = await Token.findOne({ user: user._id });

	if (existingToken) {
		const { isValid } = existingToken;
	if (!isValid) {
		throw new CustomError.UnauthenticatedError("Invalid Credentials");
    }
	refreshToken = existingToken.refreshToken;
	attachCookiesToResponse({ res, user: tokenUser, refreshToken });

	res.status(StatusCodes.OK).json({ user: tokenUser });
    return;
	}

	refreshToken = crypto.randomBytes(40).toString("hex");
	const userAgent = req.headers("user-agent");
	const ip = req.ip;
	const userToken = { refreshToken, ip, userAgent, user: user._id };

	await Token.create(userToken);

	attachCookiesToResponse({ res, user: tokenUser, refreshToken });

	res.status(StatusCodes.OK).json({ user: tokenUser });
	};



In Utils > jwtToken:

	const jwt = require('jsonwebtoken');

	const createJWT = ({ payload }) => {
		const token = jwt.sign(payload, process.env.JWT_SECRET);
	return token;
	};

	const isTokenValid = ( token ) => jwt.verify(token, process.env.JWT_SECRET);

	attachCookiesToResponse({ res, user, refreshToken }) => {
		const accessTokenJWT = createJWT({ payload: {user} })
	const refreshTokenJWT = createJWT({ payload: {user, refreshToken} })

	const oneDay = 1000 * 60 * 60 * 24;

	res.cookie('accessToken', accessTokenJWT, {
		httpOnly: true,
		secure: process.env.NODE_ENV === 'production',
		signed: true,
		maxAge: 1000,
	})

	res.cookie('refreshToken', refreshTokenJWT, {
		httpOnly: true,
		secure: process.env.NODE_ENV === 'production',
		signed: true,
		expires: new Date(Date.now() + oneDay)
		})
	};

	module.exports = {
  		createJWT,
		isTokenValid,
		attachCookiesToResponse,
	};



Logout Functionality … change ‘get’ to ‘delete’ in your routes

   Example:
      router.delete("/logout", logout);


# PASSWORDS - Forgot || Reset #

under your User.js file/model:

	// add at end of model:
	passwordTokenExpirationDate: {
		type: Date,
	},


under your authController.js:

	// add (after logout)
	const forgotPassword = async (req, res) => {
		res.send('forgot password');
	};
	const resetPassword = async (req, res) => {
		res.send('reset password');
	};

	// add your export data
	module.exports = {
		register,
		login,
		logout,
		verifyEmail,
		forgotPassword,
		resetPassword
	};


## ROUTES:  #

in authRoutes:

	// add imports:
	const {
		register,
		login,
		logout,
		verifyEmail,
		forgotPassword,
		resetPassword
	} = require('../controllers/authController')

	// add your post values:
	router.post('/reset-password', resetPassword);
	router.post('/forgot-password', forgotPassword);

	// export router
	module.export = router;


## CONTROLLERS:  #

in authController - reconfig to add email for forgotPwd:

	// add (after logout)
	const forgotPassword = async (req, res) => {
		// * ADD EMAIL INFO HERE *
		const {email} = req.body
		if(!email) {
			throw new CustomError.BadRequestError('Please provide valid email')
		}

		const user = await User.findOne({email});

		if(user){
			const passwordToken = crypto.randomBytes(70).toString('hex');
			// SEND EMAIL

			const tenMinutes = 1000 * 60 * 10; // 10min in Milliseconds
			const passwordTokenExpirationDate = new Date(Date.now() + tenMinutes);

			user.passwordToken = passwordToken;
			user.passwordTokenExpirationDate = passwordTokenExpirationDate;
			await user.save();
		}

		// Update res.send
		res
			.status(StatusCodes.OK)
			.json({'Please check your email for reset password link});
	};
	const resetPassword = async (req, res) => {
		res.send('reset password');
	};

	// add your export data
	module.exports = {
		register,
		login,
		logout,
		verifyEmail,
		forgotPassword,
		resetPassword
	};


## UTILS #

> Set up nodemailerConfig.js with your ethereal email info

### sendVerificationEmail.js #

index.js - add sendResetPasswordEmail info:

	const {createJWT, isTokenValid, attachCookiesToResponse} = require('./jwt');
	const createTokenUser = require('./createTokenUser');
	const checkPermissions = require('./checkPermissions');
	const sendVerificationEmail = require('./SendVerificationEmail');
	const sendResetPasswordEmail = require('./sendResetPasswordEmail');

	module.exports = {
		createJWT,
		isTokenValid,
		attachCookiesToResponse,
		createTokenUser,
		checkPermissions,
		sendVerificationEmail,
		sendResetPasswordEmail,
	};



authController ...

	import 'sendResetPasswordEmail'

	// then scoll down after 'if user exists...
		const user = await User.findOne({email});

		if(user){
			const passwordToken = crypto.randomBytes(70).toString('hex');
			// SEND EMAIL
			const origin = 'http://localhost:3000';
			await sendResetPasswordEmail({
				name:user.name, 
				email:user.email, 
				token:passwordToken, 
				origin,
			});

			const tenMinutes = 1000 * 60 * 10; // 10min in Milliseconds
			const passwordTokenExpirationDate = new Date(Date.now() + tenMinutes);

		user.passwordToken = passwordToken;
		user.passwordTokenExpirationDate = passwordTokenExpirationDate;

		await user.save();
		}


### sendResetPasswordEmail.js #

	// grab email
	const sendEmail = require('./sendEmail');

	const sendResetPasswordEmail = async({
		name, 
		email, 
		token, 
		origin
	}) => {
		const resetURL = `${origin}/user/reset-password?token=${token}&email=${email}`
		const message = `<p>Please reset password by clicking on the following link: <a href="${resetURL}">Reset Password</a></p>`;

		return sendEmail({
			to: email,
			subject: 'Reset Password',
			html: `<h4>Hello, ${name}</h4>
			${message}`,
		});
	}

	module.exports = sendResetPasswordEmail



### resetPasswordController #

add reset password at bottom:

	const resetPassword = async (req, res) => {
		const {token, email, password} = req.body;
		if(!token || !email || !password) {
			throw new CustomError.BadRequrestError('Please provide all valuse');
		}
		const user = await User.findOne({email});

	if(user) {
		const currentDate = new Date();

		if(user.passwordToken === token && user.passwordTokenExpirationDate > currentDate){
			user.password = password
			user.passwordToken = null
			user.passwordTokenExpirationDate = null
			await user.save()
		}
	}


		res.send('reset password')
	}



## HASH PASSWORD TOKEN #

> using crypto library
> utils: create createHash.js

	const crypto = require('crypto');

	const hashString = (string) => 
		crypto.createHash('md5').update(string).digest('hex');

	module.exports = hashString;


**index.js* - import/export

	...
	const createHash = require('./createHash');

	module.exports = {
		...
		createHash,
	}


**authController.js* - import/invoke createHash

	...
	const {
		...
		createHash,
	}

	// INVOKE IN 2 PLACES: 
	...
	const tenMinutes = 1000 * 60 * 10; // 10min in Milliseconds
			const passwordTokenExpirationDate = new Date(Date.now() + tenMinutes);

		user.passwordToken = createHash(passwordToken);
		user.passwordTokenExpirationDate = passwordTokenExpirationDate;

		await user.save();
	
	______

	const resetPassword = async (req, res) => {
		const {token, email, password} = req.body;
		if(!token || !email || !password) {
			throw new CustomError.BadRequrestError('Please provide all valuse');
		}
		const user = await User.findOne({email});

	if(user) {
		const currentDate = new Date();

		if(user.passwordToken === createHash(token) && user.passwordTokenExpirationDate > currentDate){
			user.password = password
			user.passwordToken = null
			user.passwordTokenExpirationDate = null
			await user.save()
		}
	}
	...




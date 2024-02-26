# Auth Workflow #

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
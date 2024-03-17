**JWT BASICS:** _security tokens_ [_https://jwt.io/_](https://jwt.io/)

Json Web-Token – compact URL-safe means transferring data between two parties. Authentication mechanism encoded as json.

JSON Web Token is a proposed Internet standard for creating data with optional signature and/or optional encryption whose payload holds JSON that asserts some number of claims. The tokens are signed either using a private secret or a public/private key.

JWT structure is divided into three parts: header, payload, signature & is separated from each other by dot (.), and will follow the below structure:

**Header**

	The header consists of two parts:

		The signing algorithm being used

		The type of token, which is in this case mostly “JWT”

**Payload**

	The payload usually contains the claims (user attributes) and additional data like issuer, expiration time, and audience.

**Signature**

	This is typically a hash of the header and payload sections of the JWT. The algorithm which is used to create the signature is the same algorithm mentioned in the header section of the JWT. Signature is used to validate that the JWT token wasn’t modified or changed during transit. It can also be used to validate the sender.

The header and Payload section of the JWT is always Base64 encoded.

## When should you use JSON Web Tokens?

**Here are some scenarios where JSON Web Tokens are useful:**

	Authorization: This is the most common scenario for using JWT. Once the user is logged in, each subsequent request will include the JWT, allowing the user to access routes, services, and resources that are permitted with that token. Single Sign On is a feature that widely uses JWT nowadays, because of its small overhead and its ability to be easily used across different domains.

	Information Exchange: JSON Web Tokens are a good way of securely transmitting information between parties. Because JWTs can be signed—for example, using public/private key pairs—you can be sure the senders are who they say they are. Additionally, as the signature is calculated using the header and the payload, you can also verify that the content hasn't been tampered with.

## What is the JSON Web Token structure?

In its compact form, JSON Web Tokens consist of three parts separated by dots (.), which are:

	Header

	Payload

	Signature

Therefore, a JWT typically looks like the following.

	xxxxx.yyyyy.zzzzz

Let's break down the different parts.

**Header**

The header typically consists of two parts: the type of the token, which is JWT, and the signing algorithm being used, such as HMAC SHA256 or RSA.

	For example:

	{
	"alg": "HS256",
	"typ": "JWT"
	}

	Then, this JSON is Base64Url encoded to form the first part of the JWT.

**Payload**

The second part of the token is the payload, which contains the claims. Claims are statements about an entity (typically, the user) and additional data. There are three types of claims: registered, public, and private claims.

Registered claims: These are a set of predefined claims which are not mandatory but recommended, to provide a set of useful, interoperable claims. Some of them are: iss (issuer), exp (expiration time), sub (subject), aud (audience), and others.

Notice that the claim names are only three characters long as JWT is meant to be compact.

Public claims: These can be defined at will by those using JWTs. But to avoid collisions they should be defined in the IANA JSON Web Token Registry or be defined as a URI that contains a collision resistant namespace.

Private claims: These are the custom claims created to share information between parties that agree on using them and are neither registered or public claims.

	An example payload could be:

	{
	"sub": "1234567890",
	"name": "John Doe",
	"admin": true
	}

	The payload is then Base64Url encoded to form the second part of the JSON Web Token.

Do note that for signed tokens this information, though protected against tampering, is readable by anyone. Do not put secret information in the payload or header elements of a JWT unless it is encrypted.

**Signature**

To create the signature part you have to take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that.

	For example if you want to use the HMAC SHA256 algorithm, the signature will be created in the following way:

	HMACSHA256(
	base64UrlEncode(header) + "." +
	base64UrlEncode(payload),
	secret)

The signature is used to verify the message wasn't changed along the way, and, in the case of tokens signed with a private key, it can also verify that the sender of the JWT is who it says it is.

OPTIONS:

**jsonwebtoken**

	Install:  npm install jsonwebtoken

***ADD TO HTTP STATUS CODES***

[https://www.npmjs.com/package/http-status-codes](https://www.npmjs.com/package/http-status-codes)

	Install Library:  npm install http-status-codes --save


	Usage (express 4.x)
		import {
			ReasonPhrases,
			StatusCodes,
			getReasonPhrase,
			getStatusCode,
		} from 'http-status-codes';

	response
		.status(StatusCodes.OK)
		.send(ReasonPhrases.OK);

	response
		.status(StatusCodes.INTERNAL_SERVER_ERROR)
		.send({
			error: getReasonPhrase(StatusCodes.INTERNAL_SERVER_ERROR)
		});

	response
		.status(getStatusCode('Internal Server Error'))
		.send({
			error: 'Internal Server Error'
		});

**Codes**

**Code**

**Constant**

**Reason Phrase**

	100		CONTINUE								Continue
	101		SWITCHING_PROTOCOLS				Switching Protocols
	102		PROCESSING							Processing
	103		EARLY_HINTS							Early Hints
	200		OK										OK
	201		CREATED								Created
	202		ACCEPTED								Accepted
	203		NON_AUTHORITATIVE_INFORMATION	Non Authoritative Information
	204		NO_CONTENT							No Content
	205		RESET_CONTENT						Reset Content
	206		PARTIAL_CONTENT					Partial Content
	207		MULTI_STATUS						Multi-Status
	300		MULTIPLE_CHOICES					Multiple Choices
	301		MOVED_PERMANENTLY					Moved Permanently
	302		MOVED_TEMPORARILY					Moved Temporarily
	303		SEE_OTHER							See Other
	304		NOT_MODIFIED						Not Modified
	305		USE_PROXY							Use Proxy
	307		TEMPORARY_REDIRECT				Temporary Redirect
	308		PERMANENT_REDIRECT				Permanent Redirect
	400		BAD_REQUEST							Bad Request
	401		UNAUTHORIZED						Unauthorized
	402		PAYMENT_REQUIRED					Payment Required
	403		FORBIDDEN							Forbidden
	404		NOT_FOUND							Not Found
	405		METHOD_NOT_ALLOWED				Method Not Allowed
	406		NOT_ACCEPTABLE						Not Acceptable
	407		PROXY_AUTHENTICATION_REQUIRED	Proxy Authentication Required
	408		REQUEST_TIMEOUT					Request Timeout
	409		CONFLICT								Conflict
	410		GONE									Gone
	411		LENGTH_REQUIRED					Length Required
	412		PRECONDITION_FAILED				Precondition Failed
	413		REQUEST_TOO_LONG					Request Entity Too Large
	414		REQUEST_URI_TOO_LONG				Request-URI Too Long
	415		UNSUPPORTED_MEDIA_TYPE			Unsupported Media Type
	416		REQUESTED_RANGE_NOT_SATISFIABLE	Requested Range Not Satisfiable
	417		EXPECTATION_FAILED				Expectation Failed
	418		IM_A_TEAPOT							I'm a teapot
	419		INSUFFICIENT_SPACE_ON_RESOURCE	Insufficient Space on Resource
	420		METHOD_FAILURE						Method Failure
	421		MISDIRECTED_REQUEST				Misdirected Request
	422		UNPROCESSABLE_ENTITY				Unprocessable Entity
	423		LOCKED								Locked
	424		FAILED_DEPENDENCY					Failed Dependency
	426		UPGRADE_REQUIRED					Upgrade Required
	428		PRECONDITION_REQUIRED			Precondition Required
	429		TOO_MANY_REQUESTS					Too Many Requests
	431		REQUEST_HEADER_FIELDS_TOO_LARGE	Request Header Fields Too Large
	451		UNAVAILABLE_FOR_LEGAL_REASONS	Unavailable For Legal Reasons
	500		INTERNAL_SERVER_ERROR			Internal Server Error
	501		NOT_IMPLEMENTED					Not Implemented
	502		BAD_GATEWAY							Bad Gateway
	503		SERVICE_UNAVAILABLE				Service Unavailable
	504		GATEWAY_TIMEOUT					Gateway Timeout
	505		HTTP_VERSION_NOT_SUPPORTED		HTTP Version Not Supported
	507		INSUFFICIENT_STORAGE				Insufficient Storage
	511		NETWORK_AUTHENTICATION_REQUIRED	Network Authentication Required

#
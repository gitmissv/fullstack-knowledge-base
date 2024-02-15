# Backend Security Packages #

## CORS:  Cross-Origin Resource Sharing #

	CORS mechanism supports secure cross-origin requests and data transfers between browsers and servers.  
   
   Browsers use CORS in APIs such as fetch( ) or XMLHttpRequest to mitigate the risks of cross-origin HTTP requests.

## Helmet #

	Helmet is a middleware package that protects against well known vulnerabilities.

	Install:  npm install helmet

## xss-clean:  Cross-Site Scripting #

   Cross-site scripting (xss) is a security exploit which allows an attacker to inject into a website malicious client-side code.  These attacks succeed if the Web app does not employ enough validation or encoding. 
   
   The user's browser cannot detect the malicious script is untrustworthy, and so gives it access to any cookies, session tokens, or other sensitive site-specific information, or lets the malicious script rewrite the HTML content.

## Express-Rate-Limit #

	Express-rate-limit is a middleware package that can be used to limit repeated requests to APIs and endpoints. 
   There are many reasons why excessive requests might be made to your site, such as denial of service attacks, brute force attacks, or even just a client or script that is not behaving as expected. 
   Aside from performance issues that can arise from too many requests causing your server to slow down, you may also be charged for the additional traffic. 
   
      This package can be used to limit the number of requests that can be made to a particular route or set of routes.

	Install at root of project:
		npm install express-rate-limit


# IMPORT SECURITY PACKAGES INTO YOUR APP.JS FILE

*Import after dotenv & express-async-errors*


   const helmet = require('helmet');
   const cors = require('cors');
   const xss = require('xss-clean');
   const rateLimiter = require('express-rate-limit');

*Invoke each similar to app.use(express.json())*

      app.set('trust proxy', 1);

      app.use(rateLimiter({
         windowMs: 15 * 60 * 1000,    *// 15 minutes*
         max: 100,                    *// limit each IP to 100 requests per windowMs*
      }))                             *// Add rateLimiter BEFORE express.json*

      app.use(express.json());
      app.use(helmet());
      app.use(cors());
      app.use(xss());
   

*express-rate-limit see https://www.npmjs.com/package/express-rate-limit*
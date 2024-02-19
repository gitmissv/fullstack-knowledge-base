# Cloudinary #

Cloudinary is a cloud service that offers a solution to a web app’s image management.  Easily upload images to the cloud. Automatically perform smart image resizing, cropping, and conversion without complex software. Integrate FB or Twitter profile image, etc.

      Install with npm:      npm i cloudinary

*Dashboard:*
      - Account Details:  (your credentials)
         - Cloud Name:    
         - API Key:
         - API Secret
    
Add to .env:
                
      CLOUD_NAME=
      CLOUD_API_KEY=
      CLOUD_API_SECRET=


In your app.js file, import cloudinary and config, under your fileupload:

      const fileUpload = require("express-fileupload");
      const cloudinary = require('cloudinary').v2         // ***MUST USE v2***
      cloudinary.config({
            cloud_name: process.env.CLOUD_NAME,
            api_key: process.env.CLOUD_API_KEY,
            api_secret: process.env.CLOUD_API_SECRET,
      })


Update your fileUpload to include TempFiles:

          …app.use(express.static("./public"));
          …app.use(express.json());
          app.use(fileUpload({ useTempFiles: true }));


In uploadsController.js file:

      // * IMPORTS
      const path = require("path");
      const { StatusCodes } = require("http-status-codes");
      const CustomError = require("../errors");
      const cloudinary = require("cloudinary").v2;
      const fs = require("fs");

      // * Create a Product

      const uploadProductImage = async (req, res) => {
         const result = await cloudinary.uploader.upload(
               req.files.image.tempFilePath,
                  {
                     use_filename: true,
                     folder: "file-upload",
                                }
                );
         fs.unlinkSync(req.files.image.tempFilePath);
         return res.status(StatusCodes.OK).json({ image: { src: result.secure_url } });
      };

      // * EXPORT
      module.exports = uploadProductImage;


ALTERNATE Option to Create Product (from LOCAL machine):

      const uploadProductImageLocal = async (req, res) => {
         console.log(req.files);
         if (!req.files) {
            throw new CustomError.BadRequestError("No file Uploaded");
         }

         const productImage = req.files.image;

         if (!productImage.mimetype.startsWith("image")) {
            throw new CustomError.BadRequestError("Please upload Image");
         }

         const maxSize = 1000 * 1024;

         if (productImage.size > maxSize) {
            throw new CustomError.BadRequestError(
               "Please upload image smaller than 1GB"
            );
         }

         const imagePath = path.join(
            __dirname,
            "../public/uploads" + `${productImage.name}`
         );

         await productImage.mv(imagePath);

         return res
            .status(StatusCodes.OK)
            .json({ image: { src: `/uploads/${productImage.name}` } });
         };

#

# Sending Emails #

Package *Nodemailer* = module for Node.js applications to allow easy email sending.  (https://nodemailer.com/)

      npm i nodemailer


Example
This is a complete example to send an email with plain text and HTML body using Forward Email.


      "use strict";
      const nodemailer = require("nodemailer");

      const transporter = nodemailer.createTransport({
      host: "smtp.forwardemail.net",
      port: 465,
      secure: true,
      auth: {
         // TODO: replace `user` and `pass` values from https://forwardemail.net
         user: REPLACE-WITH-YOUR-ALIAS@YOURDOMAIN.COM,
         pass: "REPLACE-WITH-YOUR-GENERATED-PASSWORD",
      },
      });

      // async..await is not allowed in global scope, must use a wrapper
      async function main() {
      // send mail with defined transport object
      const info = await transporter.sendMail({
         from: '"Fred Foo 👻" foo@example.com',                        // sender address
         to: bar@example.com, baz@example.com,                      // list of receivers
         subject: "Hello ✔",                                                                      // Subject line
         text: "Hello world?",                                                                   // plain text body
         html: "<b>Hello world?</b>",                                                 // html body
      });

      console.log("Message sent: %s", info.messageId);
   
      // Message sent: b658f8ca-6296-ccf4-8306-87d57a0b4321@example.com

      //
      // NOTE: You can go to https://forwardemail.net/my-account/emails to see your email delivery status and preview
      //       Or you can use the "preview-email" npm package to preview emails locally in browsers and iOS Simulator
      //       https://github.com/forwardemail/preview-email
      //
   }

main().catch(console.error);


## Ethereal #

https://ethereal.email/  = Ethereal is a fake SMTP service (mainly used for Nodemailer and EmailEnjine users).  Create a **FREE* account where messages will never get delivered.  **(essentially, this is a whitelisted account for testing)*

      // create new account


Connects directly to Nodemailer config:

Nodemailer configuration **in your .env file**
      const transporter = nodemailer.createTransport({
         host: 'smtp.ethereal.email',
         port: 587,
         auth: {
            user: 'garth.schowalter@ethereal.email',
            pass: 'AVtvweH6JKSAAcJFAg'
         }
      });


## SendGrid #

https://sendgrid.com/en-us. Another testing email option for API developers.  Requires a “FREE” account setup – using your own email (will need to use a valid email in order to verify…)

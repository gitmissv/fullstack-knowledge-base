# Create JWT_SECRET

To create a random 32 character string that you can use as your JWT Secret ... type in your terminal:

        node crypto.randomBytes(32).toString('hex')

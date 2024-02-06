**HTTP Messages**

HTTP _request_ message (what user sends to server)

HTTP _response_ message (what server sends back to user)

// EXAMPLE Site to review ‘inspect’ data: [http://www.course-api.com](http://www.course-api.com)


	**HTTP response status codes:
	•	100-199        Informational Responses
	•	200-299        Successful Responses
	•	300-399        Redirection Messages
	•	400-499        Client Error Responses
	•	500-599        Server Error Responses

 

**Status Codes:** [**https://developer.mozilla.org/en-US/docs/Web/HTTP/Status**](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)

>200 = request successful
>400 = error/bad request
>401 = request unauthorized
>404 = not found

**MIME Types:**
[**https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_Types**](https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_Types)

**HTTP Methods:**

>GET (default)  =  Read Data
>POST  =  Insert Data
>PUT  =  Update Data
>DELETE  =  Delete Data

**GitHub – How to download someone’s code to your computer**

	1. Navigate to GitHub repository file you want to download
		a. Select the drop-down ‘Code’ (green button)
		b. Copy/Clone the https url
	2. Open Terminal
		a. Navigate to appropriate folder
		b. Run git clone [paste url here]
		c. ‘Enter’
	3. Open in VS Code (drag-and-drop file into VSC  || OR ||  open from terminal [code .])
		a. In VSC, remove the remote url (wipe out git folder) – in order to upload your own file into github
			 **i.e. run:  **rm -rf .git**      // if it works, will remove ‘main’ from your directory




**Server ports**: (_last digits after IP Address explains how server is run:  i.e.:  443 = secure <https>; 20 = file trxfr protcol/ftp_)

>List of server ports: [https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers](https://en.wikipedia.org/wiki/List_of_TCP_and_UDP_port_numbers)

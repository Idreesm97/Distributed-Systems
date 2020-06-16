########################################################################################################
####################################        DISTRIBUTED SYSTEMS        #################################
########################################################################################################

Goals: Successfully create develop a client/server based on the .NET Web API which provides a set of 
outlined services which will be outlined below.

The server must be able to handle multiple client requests simultaneously:
	
		>A. The server must use Entity Framework, Code First, to create and manage a local database of Users 
		    (that will, in the future be moved over to a production database). 
		
		>B. The client must be able to get a TalkBack/Hello message from the server. The server will respond with “Hello World”. 
		
		>C. The client must be able to send a TalkBack/Sort message as a get request to the server with an array of integers as parameters. 
		    The server will sort the integers into ascending order and return the sorted array to the client, because – well, sorting data is tedious. 
		
		>D. The client must be able to send a User/New get request to the server which has a username string as a parameter. 
		    The server must return a string identifying if the username already exists in the database. 
		
		>E. The client must be able to send a User/New post request to the server which has a username string in the request body. 
		    The server must create a new user, generate a new GUID as an API Key, save the user to the database and return the API Key to the user. 
		    If this is the first user they should be saved as Admin role, otherwise just with User role. 
		
		>F. The client must be able to send a User/RemoveUser delete request to the server with an API Key in the header and a string username in the URI. 
		    If the server receives this request, it must check to see if the API Key is in the database and, if it is, 
		    it must check that the username and API Key are the same user and if they are, it must delete this user from the database. 
		
		>G. The client must be able to send a User/ChangeRole Post request to the server with an API Key in the header which links to an Admin role user, 
		    a string username in the body and a string role in the body. If the server receives this request, 
		    it must check to see if the API Key is in the database and whether the role is Admin, if it is, 
		    it must update the role for the given username to the role provided (User or Admin) 
		
		>H. The client must be able to send a Protected/Hello get request to the server with an API Key in the header. If the server receives this request, 
		    it must check to see if the API Key is in the database and, if it is, it must get the username associated with the API Key and send back “Hello <username>” (e.g. “Hello UserOne”). 
		
		>I. The client must be able to send a Protected/SHA1 get request to the server with an API Key in the header and a string message as a parameter. 
		    If the server receives this request, it must check to see if the API Key is in the database and, if it is, 
		    it must compute the SHA1 hash of the message and return it in hexadecimal form to the client. 
		
		>J. Somebody told the boss that SHA256 is more secure than SHA1 so the client must be able to send a Protected/SHA256 get request to the server with an API Key in the header and a string message as a parameter. 
		    If the server receives this request, it must check to see if the API Key is in the database and, if it is, it must compute the SHA256 hash of the message and return it in hexadecimal form to the client. 
		
		>K. The client must be able to send a Protected/GetPublicKey get request to the server with an API Key in the header. If the server receives this request, 
		    it must check to see if the API Key is in the database and, if it is, it must send back its RSA public key. 
		
		>L. The client must be able to send a Protected/Sign request with an API Key in the header and a string message as a parameter. 
		    If the server receives this request, it must check to see if the API Key is in the database and, if it is, 
		    it must digitally sign the message with its private RSA key and send the signed message back to the client. The client must then be able to verify that the server signed the message by using the server’s public RSA key. 
		
		>M. Finally, the client must be able to send a Protected/AddFifty get request to the server with an API Key in the header which links to an Admin role user, and three parameters comprising:  
			o An integer, encrypted using the server’s public RSA key 
			o A symmetric key (using AES encryption), encrypted using the server’s public RSA key o An IV (initialization vector) for the symmetric key, also encrypted using the server’s public RSA key 
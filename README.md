# multistorageapi
A simple API to push files to multiple storages

# Intention

I have been developing apps that has constantly required pushing files to different storage systems like S3 (an compactible ones), SFTP, WebDav, IPFS etc. This projects stems at the realization that its time I move most of the common parts of this to a common api, so I could re-use it.

# Implementation Details

1. Storage credentials and configuration
    Since the api is intended to support multiple storage backends, credential storage becomes a very important part. The implementation is as the following  

 | API            | What      | Description                   | Method | Required data | Response |  Authenticated |
|----------------|------------------------------|--------|---------------|----------|---|---------------|
|                |                              |        |               |          |   |               |                                                                                                                                                                                                                                                                                                        |
| /api/v1/keys/ | Create and store credentails | This api, would receive the access key, secret key in case of S3 or private key and username along with IP incase of SFTP etc and store the same in an encrypted form. This api would respond with a credential ID along with a decryption key and store the credentials encrypted in the database |   POST     |          {}     |       {"CredentialsID": "UUID", "CredentialKey": "A sceret decryptionable key"}   | Yes   |                
| /api/v1/keys/ | Delete a stored credential | Give a credential ID along with the decrytion key, this api would identify the credentails, test if the passed key |   DELETE     |          {"CredentialsID": "UUID", "CredentialKey": "A sceret decryptionable key"}     |       {"CredentialsID": "UUID"}   | Yes   |    


There is no update or list keys api, so the response of the create needs to be stored and cannot be retrived. 

2. Upload and CID

	This set of API's handle the file upload to the specified path 
	
| API            | What      | Description                   | Method | Required data | Response |  Authenticated |
|----------------|------------------------------|--------|---------------|----------|---|---------------|
| /api/v1/upload/ | Upload file to the specified storage |  Given the credentails ID, sceret key and the file, this api will upload the file to the destination defined in the credential | POST | "CredentialsID": "UUID", "CredentialKey": "A sceret decryptionable key","file":FILE} | {"CredentialsID":"UUID","CID":"Content Identifier"} if 200 and {"CredentialsID":"UUID","error": "Error message"} along with a 500 status code incase of error | Yes |


2. File retrival

3. Meta data and statistics

4. Authentication and Authorization

	

# Tech stack
I have a strong intention to learn node js, and as an outcome I am using nodejs. Please note, I am a begginer, and I would be very happy  to incorprace better practices in the code.

# Intended audience
I am currently not sure if I can support multiple projects. This is currently meant to serve only my needs, but post 1.0 release where it serves my purpose, I would be very happy to expand and support the needs of the community.

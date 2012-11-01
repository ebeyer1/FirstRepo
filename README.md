# Dummy API

The Dummy API is a skeleton that can be used along with DummyWebApi project template when creating a new brick. This template can be found in `C:\projects\DotNet Common\ProjectTemplates`

Since this project is an example, the base URL for all V1 calls is simple `http://127.0.0.1:81/v1/`

As stated in the project template, this example does not contain authentication, so the API can be freely hit.

##Create a New Dummy

__Request__

To create a new dummy in cloud storage, make a `POST` request to `<base_url>/dummy`. 
The request must have the following format:

    POST http://127.0.0.1:81/v1/dummy
    Content-Type: application/json
    {
        "DummyName":"dummyname",
        "Id":null,
        "Content":"dummycontent",
        "CreateDate":"2012-10-30T14:57:01.3520029Z",
        "BlobUri":null
    } 


  - _dummyName_ : Must be a valid filename
  	- Not empty
  	- Cannot be more than 500 characters
	
__Success Response__

A successful response will have the following format:


    HTTP/1.1 201 Created
    Content-Type: application/json
    Location: http://127.0.0.1:81/v1/dummy/<fileId>
    {
    	"fileId": "<fileId>",
    	"fileUri": "http://127.0.0.1:81/v1/dummy/<fileId>"
    }
  - _fileId_: Unique identifier for the uploaded dummy
  - _fileUri_: Location of the newly created resource. Use this URI to get information about the file.
  	
  __Note__: The _fileUri_ is also returned in the Location header of the response.
	
__Error Responses__

An error response will have the following format:

    HTTP/1.1 <error_http_status_code>
    Content-Type: application/json
    {
    	"message" : "<message_for_developer>"
    }

  - _message_: Message for the developer about what was wrong and how to fix it

An error response will return these https status codes for the following situations:

`400 Bad Request`
- The JSON in the request body is incorrectly formatted

`422 Unprocessable Entity`
- Any required fields have been omitted
- Any required fields are present, but empty
- Any required fields are invalid (ex: contain invalid characters, out of range, etc.)
	
##Get Dummy

__Request__

To get information about a dummy in Cloud Storage, make a `GET` request to `<base_url/dummy/<fileId>`. 
Request must have the following format:

    GET http://127.0.0.1:81/v1/dummy/<fileId> HTTP/1.1

__Success Response__

The cloud returns a success response in one of the following formats:

    HTTP/1.1 200 OK
    Content-Type: application/json
    {
    	"DummyName":"dummyname",
    	"Id":"<fileId>",
    	"Content":"dummycontent",
    	"CreateDate":"2012-10-30T14:57:01.3520029Z",
    	"BlobUri":"<uri_to_blob_storage>"
    }

  - _DummyName_: Name of the dummy in Cloud Storage
  - _Id_: Unique identifier for the uploaded dummy
  - _Content_: the text content stored in the cloud
  - _CreateDate_: The DateTime the dummy was put in storage
  - _BlobUri_: The URI that can be used to access the uploaded content

__Error Responses__

An error response will have the following format:

    HTTP/1.1 <error_http_status_code>
    Content-Type: application/json
    {
       "message" : "<message_for_developer>"
    }

  - _message_: Message for the developer about what was wrong and how to fix it

An error response will return these http status codes for the following situations:

`404 Not Found`
- `<fileId>` does not exist

##Update Dummy

__Request__

To update an existing file in Cloud Storage, make a `PUT` request to `<base_url>/dummy/<fileId>`. 
The request must have the following format:

    PUT http://127.0.0.1:81/dummy/<fileId> HTTP/1.1
    Content-Type: application/json
    {
    	"DummyName" = "dummyname",
    	"Content" = "updated content",
    	Id = <fileId>
    }

  - _DummyName_: Must be the same as the dummy being updated
  - _Id_: Must be the same as the dummy being updated

__Success Response__

A successful response will have the following format:

    HTTP/1.1 200 OK
    Content-Type: application/json
    {
    	"fileId" : "<fileId>"
    }

  - _fileId_: Unique identifier for the uploaded file

__Error Responses__

An error response will have the following format:

    HTTP/1.1 <error_http_status_code>
    Content-Type: application/json
    {
       "message" : "<message_for_developer>"
    }

  - _message_: Message for the developer about what was wrong and how to fix it

An error response will return these http status codes for the following situations:

`400 Bad Request`
- The JSON in the request body is incorrectly formatted

`422 Unprocessable Entity`
- Any required fields have been omitted
- Any required fields are present, but empty
- Any required fields are invalid (ex: contain invalid characters, out of range, etc.)

##Delete a Dummy

__Request__

To delete a dummy in Cloud Storage, make a `DELETE` request to `<base_url/dummy/<fileId>`. 
The request must have the following format:


    DELETE http://127.0.0.1:81/dummy/<fileId> HTTP/1.1

__Success Response__

The cloud returns a success response if the item has been successfully deleted.

    HTTP/1.1 200 OK


__Error Responses__

An error response will have the following format:

    HTTP/1.1 <error_http_status_code>
    Content-Type: application/json
    {
       "message" : "<message_for_developer>"
    }

  - _message_: Message for the developer about what was wrong and how to fix it

An error response will return these http status codes for the following situations:

`404 Not Found`
- `<fileId>` does not exist

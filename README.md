# FuelSDK-Python-Wrapper
Simplify and improve the FuelSDK for Salesforce Marketing Cloud (ExactTarget).

## Overview
The Fuel SDK for Python provides easy access to ExactTarget's Fuel API Family services, including a collection of REST APIs and a SOAP API. These APIs provide access to ExactTarget functionality via common collection types such as array/hash.

## Installation

The Fuel SDK for python can be easily installed from the [Python Package Index](https://pypi.python.org/pypi) using the [pip](https://pip.readthedocs.org) command. Pip is a tool for installing and managing Python packages.

```
pip install FuelSDK-Wrapper
```

## Getting Started

### Configuring

You must configure your access tokens and details for the Fuel SDK in one of the following two ways.

1. Copy the included `config.python.template` file to `config.python` in either `~/.fuelsdk/` or within this python module.
2. Add environment variables:
    * `FUELSDK_CLIENT_ID` (required)
    * `FUELSDK_CLIENT_SECRET` (required)
    * `FUELSDK_APP_SIGNATURE`
    * `FUELSDK_DEFAULT_WSDL`
    * `FUELSDK_AUTH_URL`
    * `FUELSDK_WSDL_FILE_LOCAL_LOC`

Edit `config.python` or declare environment variables so you can input the ClientID and Client Secret values provided when you registered your application. If you are building a HubExchange application for the Interactive Marketing Hub then, you must also provide the Application Signature (`appsignature` / `FUELSDK_APP_SIGNATURE`).
The `defaultwsdl` / `FUELSDK_DEFAULT_WSDL` configuration must be [changed depending on the ExactTarget service](https://code.exacttarget.com/question/there-any-cetificrate-install-our-server-access-et-api "ExactTarget Forum").
The `authenticationurl` / `FUELSDK_AUTH_URL` must also be [changed depending on service](https://code.exacttarget.com/question/not-able-create-accesstoken-when-clientidsecret-associated-preproduction-account "ExactTarget Forum").
The `wsdl_file_local_loc` / `FUELSDK_WSDL_FILE_LOCAL_LOC` allows you to specify the full path/filename where the WSDL file will be located on disk, if for instance you are connecting to different endpoints from the same server.

If you have not registered your application or you need to lookup your Application Key or Application Signature values, please go to App Center at [Code@: ExactTarget's Developer Community](http://code.exacttarget.com/appcenter "Code@ App Center").


| Environment | WSDL (default) | URL (auth) |
| ----------- | -------------- | ---------- |
| Production  | https://webservice.exacttarget.com/etframework.wsdl | https://auth.exacttargetapis.com/v1/requestToken?legacy=1 |
| Sandbox     | https://webservice.test.exacttarget.com/Service.asmx?wsdl | https://auth-test.exacttargetapis.com/v1/requestToken?legacy=1 |


## Example Request

### Code

All ExactTarget objects exposed through the Fuel SDK begin with be prefixed with "ET\_".  Start by working with the ET_List object:

```python
# Add a require statement to reference the Fuel SDK's functionality:
import FuelSDK

# Next, create an instance of the ET_Client class:
myClient = FuelSDK.ET_Client()

# Create an instance of the object type we want to work with:
list = FuelSDK.ET_List()

# Associate the ET_Client to the object using the auth_stub property:
list.auth_stub = myClient

# Utilize one of the ET_List methods:
response = list.get()

# Print out the results for viewing
print 'Post Status: ' + str(response.status)
print 'Code: ' + str(response.code)
print 'Message: ' + str(response.message)
print 'Result Count: ' + str(len(response.results))
print 'Results: ' + str(response.results)
```


### Example Output

```
Retrieve Status: True
Code: 200
Message: OK
MoreResults: False
Results Length: 1
Results: [(List){
   Client =
      (ClientID){
         ID = 113903
      }
   PartnerKey = None
   CreatedDate = 2013-07-29 04:43:32.000073
   ModifiedDate = 2013-07-29 04:43:32.000073
   ID = 1966872
   ObjectID = None
   CustomerKey = "343431CD-031D-43C7-981F-51B778A5A47F"
   ListName = "PythonSDKList"
   Category = 578615
   Type = "Private"
   Description = "This list was created with the PythonSDK"
   ListClassification = "ExactTargetList"
 }]
```

## ET\_Client Class

The ET\_Client class takes care of many of the required steps when accessing ExactTarget's API, including retrieving appropriate access tokens, handling token state for managing refresh, and determining the appropriate endpoints for API requests.  In order to leverage the advantages this class provides, use a single instance of this class for an entire session.  Do not instantiate a new ET_Client object for each request made.

## Responses

All methods on Fuel SDK objects return a generic object that follows the same structure, regardless of the type of call.  This object contains a common set of properties used to display details about the request.

| Parameter | Description                                                     |
| --------- | --------------------------------------------------------------- |
| status    | Boolean value that indicates if the call was successful         |
| code      | HTTP Error Code (will always be 200 for SOAP requests)          |
| message   | Text values containing more details in the event of an Error    |
| results   | Collection containing the details unique to the method called.  |

Get Methods also return an addition value to indicate if more information is available (that information can be retrieved using the getMoreResults method):

 - moreResults - Boolean value that indicates on Get requests if more data is available.


## Samples

Find more sample files that illustrate using all of the available functions for ExactTarget objects exposed through the API in the objsamples directory.

Sample List:

* [BounceEvent](https://github.com/ExactTarget/FuelSDK-Python/blob/master/objsamples/sample_bounceevent.py)
* [Campaign](https://github.com/ExactTarget/FuelSDK-Python/blob/master/objsamples/sample_campaign.py)
* [ClickEvent](https://github.com/ExactTarget/FuelSDK-Python/blob/master/objsamples/sample_clickevent.py)
* [ContentArea](https://github.com/ExactTarget/FuelSDK-Python/blob/master/objsamples/sample_contentarea.py)
* [DataExtension](https://github.com/ExactTarget/FuelSDK-Python/blob/master/objsamples/sample_dataextension.py)
* [Email](https://github.com/ExactTarget/FuelSDK-Python/blob/master/objsamples/sample_email.py)
* [List](https://github.com/ExactTarget/FuelSDK-Python/blob/master/objsamples/sample_list.py)
* [List > Subscriber](https://github.com/ExactTarget/FuelSDK-Python/blob/master/objsamples/sample_list_subscriber.py)
* [OpenEvent](https://github.com/ExactTarget/FuelSDK-Python/blob/master/objsamples/sample_openevent.py)
* [SentEvent](https://github.com/ExactTarget/FuelSDK-Python/blob/master/objsamples/sample_sentevent.py)
* [Subscriber](https://github.com/ExactTarget/FuelSDK-Python/blob/master/objsamples/sample_subscriber.py)
* [TriggeredSend](https://github.com/ExactTarget/FuelSDK-Python/blob/master/objsamples/sample_triggeredsend.py)
* [UnsubEvent](https://github.com/ExactTarget/FuelSDK-Python/blob/master/objsamples/sample_unsubevent.py)

## Development on FuelSDK-Python

If you would like to help contribute to the FuelSDK-Python project, checkout the code from the [GitHub project page](https://github.com/ExactTarget/FuelSDK-Python). The use of [virtualenvwrapper](http://virtualenvwrapper.readthedocs.org/) is highly recommended. After installing virtualenvwrapper you can run the following commands to setup a sandbox for development.

```
git clone git@github.com:ExactTarget/FuelSDK-Python.git
mkvirtualenv FuelSDK-Python
cd FuelSDK-Python
pip install -r requirements.txt
```

You will then have a sandbox which includes all dependencies for doing development on FuelSDK-Python.

## Requirements

Python 2.7.x

Libraries:

* pyjwt
* requests
* suds

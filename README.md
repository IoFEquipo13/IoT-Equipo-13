
video https://www.youtube.com/watch?v=NYGhhhUtPHM

##Introduction 1
###1.1 Purpose
As the world keeps growing with its population, the need for transportation grows too. With this being said, it is no longer a necessity to have something for us to go anywhere we want to. But that’s just not it, cities are having trouble with the amount of traffic the citizens have to endure on a daily basis or the amount of time they waste looking for a space to park their cars. Which is why, we came up with a solution: Space it. A mobile application made specifically for all of those people that want to make their life’s a bit easier. On your way to school or your job, Space it will tell you where to go. Using pop up notifications, once you are near your destination, Space it will do the rest. An application with low resources and with high efficiency. By simply filling the application with our schedule, we will tell you the zones most near to them with available parking spaces. Our application is currently focused in private parking lots, but hopefully in the future it will escalate to the city as a whole.
###1.2 Scope
Our application will tell you , based on a recommendation algorithm, the spaces available for you to park your car, based on the nearest zone. The benefits will be: saving time, no more wasted gas and a friendly user experience with a smart parking lot application. 
Objective: By taking a snapshot of the license plate of all the users that enter the parking lot we will make a “match” to define which user has entered the parking lot and with this we will provide the correct algorithm for the correct user.
##Product Perspective
Right now in our city, we have a smart parking lot, but this one consists only in signs  and sensors that simply change color when a parking space is being used. This is what citizens know as “Smart Parking lot” and as the design it is not so different from ours , the main difference comes with the mobile application, which will make ours way more efficient.


###Product Functions
We will use Facebook Log in as our user log in, withdrawing their name and email to our database. The user must write their license plate too to complete the registration.
Our application must tell to the user accurately, which zone is the nearest and the amount of spaces available.
###User Characteristics
Space It is directed mainly for all the users that use a private parking lot like colleges and industries. Therefore they must need a parking space for their cars or whichever type of transportation they use to go their destination.

###General Constraints
Space it will require an Android system with the following hardware specifications:
Dual-Core 1Ghz or faster processor.
512 MB RAM 
Android OS 4.1 jelly bean or superior.
###Functional Requirements
 
####System Feature #1 Facebook Log in
It consists in, with a simple log in button, the user automatically will be logged in , in our system, and we will use their name and their email for our database. Along with that we will have a space in which the user will have to write their license plate.
####System Feature #2 Zone Selection
The user will be able to select their desired zone 
####System Feature #3 Recommendation Algorithm
Through pop up notifications our application will tell the user which zone is the nearest to him and the amount of places available



###Non-Functional Requirements

####Performance
The application, in just a few seconds, will drop a notification indicating the best zone to park and the number of parking spaces available in that area. 

####Reliability
Only the user will be able to access and modify their information. 
###Availability
The system will be available for organizations that count with a private parking lot.
###Security
Since all of the information will be stored in our server, it is highly unlikely that someone can steal information. 

###Maintainability
With the objective of making an effective app, it has been created different states for each parking space. A parking space can be:
Available: 
Occupied:
Reserved: 

###Portability
Space It is an application developed for smartphones with Android OS. However, it will be available for IOS very soon.
















































#Problem definition
It is common to see in a daily basis that in places such as parking zones, there is a problem that peoples deals with. When they arrive, they try to look for the nearest spot from their destination. But this is not as easy as that when it is an enormous place on a side with a lot of taked slots. This means people going round and round, wasting their time, gasoline and this whole set is neither pragmatic nor efficient in any way.

##System
The system develop in here will be explained in the next points. Consist in making a orchestration of 4 elements, an edison, an app, a backend API and a plate recognition algorithm  

###Edison (Git https://github.com/IoTEquipo13/Edison)
Once the user has entered the parking lot, we’ll send a snapshot of their plates to a server, which will process the image’s plates, that’s how we can identify who user is entering the parking lot. The edison will send the image to the plate recognition algorithm.

###Android (Git https://github.com/IoTEquipo13/APP)
This consists of an App where the user can register his basic information and preferences about parking zones and then, when he arrives to the parking zone, a photograph of his plates will be sent to the API and in return, with a Push Notification, he will be notified about the useful information that will help him know the best place to park on.

###Backend (Git https://github.com/IoTEquipo13/API)
The place where all the elements are connected, this is where the endpoints are

####Create User:
*Method: POST
	*URL: https://greenheadapi.azurewebsites.net/api/user/register/
	*JSON: *{"Plate":"Expreso","Photo":"ashd","Name":"Poncho","Mail":"miguelpg_95@hotmail.com","PrefSegment":{"0":"Zone1","1":"Zone2","2":"Zone1","3":"Zone2","4":"Zone1","5":"Zone2"},"Condition":"Normal"}

####Add License Plate
	*Method: POST
	*URL: https://greenheadapi.azurewebsites.net/api/user/AddPlate/{IdUsuario}
	*JSON: "Plate2"

####Look for User
	*Method: GET
	*URL: https://greenheadapi.azurewebsites.net/api/user/getUser/{Placa}

####Update a Spot on a Device
	*Method: POST
	*URL: https://greenheadapi.azurewebsites.net/api/device/update
	*JSON: {"DeviceId":"Zona1","PlaceId":"1","Status":"0"}

####Get Parking Recommendation
	*Method: GET
	*URL: https://greenheadapi.azurewebsites.net/api/place/getzone/{Placa}

####Register to Notifications
	*Method: POST
	*URL: https://greenheadapi.azurewebsites.net/api/register/post
	*JSON: “{“handle”: IdGCM}”

####Get Notification Id:
	*Method: POST
	*URL:https://greenheadapi.azurewebsites.net/api/register/put/{IdQueRegresaElMetodoAnterior}
	*JSON: {"Platform":"gcm","Handle":"{IdGCM}"} 
	

####Send Notification to specific user
	*Method: POST
	*URL: https://greenheadapi.azurewebsites.net/api/notifications/Post/?Id={UsuarioQueEnvia}&pns={plataformaALaQueEnvia}&to_tag={UsuarioQueRecive}
	*JSON: “mensaje a ser enviado”
	

###Plate recognition
When the user arrives at the entrance of the parking zone, a camera will take a snapshot of their plates and will sent it to a remote server which is responsible of processing the plate with OpenALPR  and send it to the API responsible of analyze it with its preferences so it can detect such plates and give the output back.
This algorithm runs over ubuntu 14.04 in an external server.

OpenALPR is an open source Automatic License Plate Recognition library  that analyzes images and video streams to identify license plates.

# Meal on Wheels
This programme is to develop an android application and website, which will create a database of the Eating Joints falling with the Origin and Destination Points of the journey and placing the orders as per the available Menu at particular​ ​ Eating​ ​ Joint​ ​ with​ ​ time​ ​ of​ ​ Service.

## Brief Solution:

We propose to develop a platform comprising of an android application and website which will enable a traveller to search and order food from eating joints which are located throughout the route to their destination. 

Our platform would include user authentication and thus would enable us to maintain a user profile to deliver a more personalised experience to our users. We will get the current location of the user using GPS (with the option of entering it manually) and will ask for a destination, after which we will display the list of eating joints which are located near their current route arranged in increasing order of their time of arrival. The user can select the preferred eating joint based on their requirements and will be able to place their order with the time of service after selecting food items from the menu of the selected eating joint. 


## Description of Technology:

### Structure of Database: 
* We will be using MySQL database management system for our data storing requirements. 
* Our data base will consist of tables for storing information about the users and various eating joints.
* The user specific table will consist of data points such as name, mobile, email, unique ID etc.
* Information about eating joints will comprise of name, unique code and location (in the form of latitude and longitude). 
* We will be storing the menus of various eating joints in separate JSON files whose link will be stored along with other     information of the eating joints in the concerned table.

### Functionality of app:
* The user will have the option of logging-in via their mobile number or through their Facebook/Google account.
* Upon successful authentication, the user will have to enter their destination by Entering address or by placing marker on  the map.
* The current location will be fetched by our app through GPS or it can be Entered manually by the user. 
* The shortest path will then be calculated by the Google directions API. The polylines that the google’s API will throw would enable us to calculate nodes along the path.
* Considering these nodes as centres of circles of radius 2km, we will search for eating joints located within them.We would achieve this by getting the latitude and longitude of these nodes and then searching in our database for the qualified eating joints. 
* These joints will be displayed in a map and the user will be to view the list of all the eating joints sorted according to their distance from the current location.
* After selecting the preferred eating joint, the user will be provided with the menu of the selected eating joint. 
* The user will then be able to select food items and place their order with the eating joint. 
* The order will be confirmed by the respective eating joint through confirmation call. The user can then directly start navigation to the concerned eating joint.


Suppose r1, r2, r3, r4 etc. are the locations of eating joints lying within the circle. We will then find the points having latitudemin(E_S), latitudemax(E_N), longitudemin(E_W) and longitudemax(E_E) lying on the circumference of circle using the following formula:
φ2 = asin( sin φ1 ⋅ cos δ + cos φ1 ⋅ sin δ ⋅ cos θ )
λ2 = λ1 + atan2( sin θ ⋅ sin δ ⋅ cos φ1, cos δ − sin φ1 ⋅ sin φ2 )
Bearing: 0 gives max longitude 
Bearing 180 gives min longitude 
bearing 90 gives min latitude 
bearing -90 gives max latitude 
(all angles in radians)

where    φ is latitude, λ is longitude, θ is the bearing (clockwise from north), δ is the angular distance x/R; x being the radius of circle, R the earth’s radius.

![Image of Overview]
(https://github.com/Not-Decided/Meal-on-Wheels/blob/master/Overview.png)
Following is the implentation of above formula in javascript:

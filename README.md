# Food-Delivery_Application

Food Delivery Application:
It’s an app for delivering food like Zomato, Swiggy etc.
Step:1
We will try to understand the basic flow of food delivery.

There should be a panel(API) from where the driver will be logging in.
There should be a panel(API) from where the User will be logging in.
There should be a panel(API) from where the merchant/Restaurant will be logging in.
First of all, we can have multiple tables for all of these. If we have multiple applications that there should be different tables/ or we can keep the same table for all types of users. Both approaches are correct depending upon the architecture of the project.
How are we gonna Proceed for now?
We will be creating 1 service for all users (MODULE : UserService). That means one API will do the login for all. And we will be having security in it.
Once the user is onboarded will be sending the information to the kafka and consumers will be receiving this information.
Who all can be the consumers?
Notification Service (MODULE:NotificationService): Which will be sending notifications, SMS or MAILs. We will be creating this.
Karma Service : which will check if the user is a robot, or fraud etc.


Step:2
Try to understand the home pages of all (user ,driver,merchant)

What User/Driver/Merchant will see?
User will have a list of restaurants near by him.(API- for user home page which will load restaurants near him.) Now the user wants complete information so not everything will not be done by UserService. There should be MerchantService which will be keeping all information related to restaurants.

Driver will have one API when he wants to go online and what will be the area he will cover and for how many hours. All tasks will be handled by DriverService.

Merchant will have an API to upload the restaurant details like the location of the restaurants and name and classification, Opening timings etc. 
Then he should also get an api to upload dishes and their costs.
Step:3
What will be the order flow?
Users will come and order something as cash on delivery because we are not going in the payments flow.(OrderService) module will be handling the order and we need to see how this order will be assigned to the driver. And publish some data on kafka. Merchant on which the order has been placed will listen on MerchantService and start preparing. DriverService will listen to it and will start looking for the available drivers. And all the information related to the order will be present in the database of OrderService.

Step:4
How will the order flow from order picked up to Order delivered?
Once the order has been assigned to some driver. The driver will first accept the order, go to the restaurant and pick up the order, move to the user location and this information will get published in kafka step by step and whoever wants to listen to this can listen. OrderService in our case will be listening to all the details and updating to the user. Once the driver reaches the user, He will mark the order as completed and some money which has already been decided will be shown up in the My-Earning Section. Later on, This can be settled among the application and driver.
 

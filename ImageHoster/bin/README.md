# ImageHoster
***Problem Statement***
In this course, you have learnt about software engineering topics ranging from version control to extreme programming, as well as backend development using Spring Boot, JPA, and PostgreSQL to build a backend application.

 

In this assignment, you’ll apply everything you have learnt in course 4 to build an image hoster similar to Imgur, one of the top 100 most visited websites in the world.

 

***Goals of This Assignment***
Through working on the image uploader, you’ll get a chance to experience what it is like to join an engineering team as a new, junior software engineer. Specifically, you’ll get a chance to familiarize yourself with the codebase by fixing a few bugs in the codebase. You’ll also get a chance to implement a few well-defined features to the image uploader and improve its functionalities.

Lastly, this project will also introduce you to new concepts to Spring MVC, JPA, PostgreSQL and unit testing. Some of these concepts will be explained to you, and some concepts, you need to Google and Stack Overflow to learn those concepts on your own. This experience will further enhance the experience of joining a new team as a junior software developer as mentioned above.

 

***Stub File***
As all of you have implemented the ‘Image Hoster’ project given in MVC architecture and Database & ORMs assessments, you will continue working on the same project as a part of this assignment. 
Let us discuss in brief, the features implemented in the ‘Image Hoster’ project till now.

The application runs on localhost and the user is redirected to the landing page of the application displaying all the images in the application.
A new user can register in the application by entering the details such as username, password, full name, email address, and mobile number, and after the successful registration, he is redirected to the login page.
The user can log in the application by entering the username and password, and after successful login to the application, the user is redirected to the user homepage, displaying all the images in the application.
After a user successfully logs in the application, he can click on the title of any image and the image details will be displayed including the description and tags of the image, along with the option to edit and delete the image.
A user can also upload the image by entering the details such as image title, description, image file, and tags related to the image.
You may register in the application and upload the images in the application, to check all the features discussed above.
Instructions:
You must manually create a database named ‘imageHoster’ in PostgreSQL with the user as ‘postgres’ using pgAdmin as the UI.
Change the username and password in the stub file in the ‘src/main/java/imageHoster/config/JpaConfig.java’ file and ‘src/main/resources/META-INF/persistence.xml’ file according to your PostgreSQL username and password. 
Note that it is mandatory to assign at least one tag/category to an image while you upload the image. If you do not assign any tag to the image, the image will get uploaded in the application. But when you try to edit the image, the application throws an error. 
***To-Do Tasks***
***Part A: Fixing Issues***
***1. Image upload issues:*** 

If you upload an image with the same exact title as of a previously uploaded image, it will get uploaded. But then, if you try to navigate to one of the images with the same title, the image uploader will display an error.
Please fix this issue, so that the application should not show an error and take you to respective image’s page.
Please see more details of this issue on Github.
 

2. After logging into the application, it is possible to edit/delete the image which is posted by some other user. This is a bug in the application. Now, fix this bug in the application, such that only the owner of the image can edit/delete the image. Check this link for more details.

If the owner of the image is trying to edit the image, you must return the ‘images/edit.html’ file, thus enabling the user to edit the image. But if the non-owner of the image is trying to edit the image, return the ‘images/image.html’ file displaying all the details of the image and print the message ‘Only the owner of the image can edit the image’. Carefully add all the required attributes in the Model type object needed by ‘images/image.html’ file.
If the owner of the image is trying to delete the image, the image is deleted and the user must be redirected to the web page displaying all the images. But if the non-owner of the image is trying to delete the image, return the ‘images/image.html’ file displaying all the details of the image and print the message ‘Only the owner of the image can delete the image’. Carefully add all the required attributes in the Model type object needed by ‘images/image.html’ file.
***Part B: Implement a new feature***
After fixing the above issues, please implement the following features into the image uploader application:

***1.  Password Strength***

Up till now, there is no check on the strength of the password entered by the user at the time of registration. Let us try to keep a check on the strength of the password entered by the user at the time of registration. You need to implement a feature wherein the password entered by the user must contain at least 1 alphabet (a-z or A-Z), 1 number (0-9) and 1 special character (any character other than a-z, A-Z and 0-9). The user must only be registered if the password contains 1 alphabet, 1 number, and 1 special character. And after successful registration, you must directly return 'users/login.html' file. Otherwise, the user must not be registered and again return the ‘users/registration.html’ file. You also need to display a message ‘Password must contain at least 1 alphabet, 1 number & 1 special character’. Carefully add all the required attributes in the Model type object needed by ‘users/registration.html’ file.
Hint:

How to display the error message?

Declare and initialize a string with the message in the Controller logic as shown below:
String error = "Password must contain atleast 1 alphabet, 1 number & 1 special character"

Add the above string specifying the password type error in the Model type object with ‘passwordTypeError’ as the key.
Display a message in ‘users/registration.html’ file with an if condition.
If the Model type object contains the string representing the password type error, only then you should display the message.
Else, the message should not be displayed. Uncomment the following instruction given below in registration.html file to display the message with if condition.
<div th:if="${passwordTypeError}">Password must contain atleast 1 alphabet, 1 number & 1 special character</div>

Note that the test cases are designed in such a way that you need to add the message "Password must contain at least 1 alphabet, 1 number & 1 special character" with the key as ‘passwordTypeError’ for the test cases to pass.
 

***2.  Comments***

Now, implement a feature wherein a user can add a comment to any image in the application after he is logged in the application, and, to implement this feature, you’ll have to add the following to the image uploader application:

Create a Comment model class. The model class contains the following attributes:
id - Datatype should be int. It should be a primary key. Also explicitly mention the column name as ‘id’ to be created in the database.
text - Datatype should be a string. Note that this column can have text-based data that will be longer than 256 characters.
createdDate - Datatype should be LocalDate.
user - It should be of type User. The ‘comment’ table is mapped to ‘users’ table through this attribute. One user can post multiple comments but one comment should belong to one user. Write the suitable annotation to map the ‘comment’ table to ‘users’ table through this attribute.
Image - It should be of type Image. The ‘comment’ table is mapped to ‘images’ table through this attribute. One image can have multiple comments but one comment can only belong to one image. Write the suitable annotation to map the ‘comment’ table to ‘images’ table through this attribute.
Implement a controller class method  that maps to the POST request URL ‘/image/{imageId}/{imageTitle}/comments’ for creating a new comment. After persisting the comment in the database, the controller logic must redirect to the same page displaying all the details of that particular image. Redirect to ‘showImage()’ method in ‘ImageController’ class.

You can obtain the request parameters from the client request using @RequestParam annotation. And obtain the dynamic parameter in the request URI using the annotation @PathVariable. You can read more about @PathParam and @RequestParam in the following links:

@RequestParam vs @PathVariable
How to explicitly obtain post data in Spring MVC?
Implement the required service logic and the Repository logic for the comment feature.

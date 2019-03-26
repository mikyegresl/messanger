# Android Messenger

## 1. Objective
Our term project application mainly focuses on educational purpose.In order to learn Android programming using Java 
language we implemented open-source chatting program for Android operating system.

## 2. Description
The main function of chat application is sending/receiving messages in realtime. To deliver messages in realtime, Firebase
Realtime Database was used. It allows to listen to any changes occuring in database which is very helpful in Messenger.
You can also send pictures from Gallery written in Kotlin. It contains lots of beautiful images. In search field, type
appropriate keyword and plenty of images related to your query will be provided.

## 3. Implementation
Below are the implementation details containing information about application functions and database implementations.

### 3.1 User Interface

#### 3.1.1 Application UI
We created user-friendly GUI, where it is not complicated to intuitively use chatting and contact search. 
This is the final version of UI. UI implementation is free of third-party APIs and libraries like Scaledrone or Bootstrap.
Every UI component is coded in XML files and only native Android Studio tools were used for this purpose.

### 3.2 Functions

#### 3.2.1 Sign Up/Sign In
First and foremost, a user must sign in to use our chat app. If you do not have an account yet, press on image button
on the right of the form to create a new account.

![Sign Up](https://github.com/mikyegresl/Android_Messenger/blob/master/screens/sign_up.png)

If all required fields are filled and are valid, a new account entry is created in Firebase Authentication mechanism.  
It looks like:

![Firebase Authentication](https://github.com/mikyegresl/Android_Messenger/blob/master/screens/authentication_json.png)

Next, to sign in, enter your email address and password.

![Sign In](https://github.com/mikyegresl/Android_Messenger/blob/master/screens/sign_in.png)

#### 3.2.2 Contact List
After singing in, user may add a person to chat with. To do this, enter valid email address of registered user into 
search field and tap on mangifier icon. If account is valid and does exist in database, a new recycler view entry 
will be created with full name and email address displayed on it.

![Contact List](https://github.com/mikyegresl/Android_Messenger/blob/master/screens/contact_list.png)

#### 3.2.3 Exchange Messages
Basically, message exchange in realtime is constantly pushing information into database and fetching from it. For example,
if current user sends some message, a new message entry is created in database and then is read by Firebase 
asynchronous listeners. In UI, messages of current user are displayed green and attached to right side of the window, while
messages of a peer are displayed from left side and in blue color respectively.

![Chat](https://github.com/mikyegresl/Android_Messenger/blob/master/screens/chat.png)

#### 3.2.4 Send Pictures from Gallery

You cannot send your pictures from gallery in our application, instead, we implemented online gallery with plenty of
beautiful pictures. To share some thematic image, type keywords related to the picture in search field.  

![Gallery 1](https://github.com/mikyegresl/Android_Messenger/blob/master/screens/gallery_1.png)  

![Gallery 2](https://github.com/mikyegresl/Android_Messenger/blob/master/screens/gallery_2.png)  

This is how it looks in chat:  

![Gallery 3](https://github.com/mikyegresl/Android_Messenger/blob/master/screens/gallery_3.png)  

For this image I typed 'hockey' in Gallery:  

![Gallery 4](https://github.com/mikyegresl/Android_Messenger/blob/master/screens/gallery_4.png)  

### 3.3 Database

#### 3.3.1 Users
We used Firebase Realtime Database to handle authentication purpose. The identifiers are user email address and
password. Whenever a new account is created, user ID is generated by Firebase push() function.
It is based on current timestamp.

![Users Database](https://github.com/mikyegresl/Android_Messenger/blob/master/screens/users_json.png)

#### 3.3.2 Chats
These UIDs are needed in order to connect people who are talking to
each other. The logic is as follows: in database each chat is represented as one-to-one relationship concatenating UIDs
of two chat members. So, chat ID itself is a unique identifier representing a single message container but on the other 
hand, it is just a string concatenating UIDs of this chat members. To keep in mind that some chat already exists with
messages attached to it, whenever a new chat is created, we need to check if a chat contains current user ID.

#### 3.3.3 Messages
Message entry in database contains following fields:
* message ID        //unique message identifier
* sender ID         //to know which user among two sent message
* sender email
* recipient email
* content           //content of message
* timestamp         //date and time when sent
* type              //can be text, image or link
* url               //none if text

![Users Database](https://github.com/mikyegresl/Android_Messenger/blob/master/screens/messages_json.png)
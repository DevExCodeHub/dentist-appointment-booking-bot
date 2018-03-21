# Dentist-Appointment-Booking-Bot

This is a simple chatbot that can assist you in booking dentist appointments. Functionalities include greeting users in their timezone, simplified dental appointment booking and also introduces user to entities-regular expression pattern matching.  

## IBM Watson® Conversation
IBM Watson® Conversation is a question-and-answer system that provides a dialog interaction
between the conversation system and users. This style of interaction is commonly called a
chatbot

Now, let's build the conversation!

## Task 1: Login to your IBM Cloud account & create Conversation service

1. Login to your IBM Cloud account, if you don't have one already you can [singup here](https://ibm.biz/BdZift).
2. Open the Catalog, click on **Watson** to refine search.
3. Scroll down and click on **Conversation** service.
4. Click on **Create** to create an instance of the service. Make sure you choose an **organization** and **space**.
5. Click on **Launch tool** to open the tool.

![](https://github.com/Deemaalamer/Dentist-Appointment-Booking-Bot/blob/master/images/bot1.gif)

## Task 2: Create your bot workspace
1. Click on **(+) Create** to create the wrokspace.
2. Name your bot '**Dental Appointment Booking Bot**'

![](https://github.com/Deemaalamer/Dentist-Appointment-Booking-Bot/blob/master/images/bot2.gif)

## Task 3: Create your intents
An intent is a group of examples of things that a user might say to communicate a specific goal
or idea. To identify intents, start with something that a user might want and then list the ways
that the user might describe it.

Here we are going to crete two intents. For each intent, we will add examples to train the conversation for intent recognition.

1. Add the first inetent and call it **#book_appointment**
2. Click **Create** to create the intent.
3. Add user examples such as: Book an appointment, Book appointment, Can you pls help me book an appointment, cavity in my tooth, Help me book an appointment, I need to book an appointment immediately, I have a tooth pain, My tooth is aching, I need to book an appointment immediately... etc

![](https://github.com/Deemaalamer/Dentist-Appointment-Booking-Bot/blob/master/images/bot3.gif)

4. Add the second intent and call it **#thanks**, this is to detect when the user is thanking the bot.
5. Click **Create** to create the intent.
6. Add user examples such as: Thank you, Thank you very much, Thanks, Thanks a lot.. etc

![](https://github.com/Deemaalamer/Dentist-Appointment-Booking-Bot/blob/master/images/bot4.gif)

## Task 4: Create your entities
Entity is a portion of the user's input that you can use to provide a
different response to a particular intent. Click Entities. On the Entities page, click Create new.

Each entity definition includes a set of specific entity values that can be used to trigger different
responses. Each value can have multiple synonyms that define different ways that the same value
can be specified in user input. Create entities to represent to the application what the user wants to access. Fuzzy logic is a
feature that allows Watson Conversation to accept misspelled words. You can enable this feature
at the entity level.

1. Under **My entities tab**, add your first entity and call it **@personal_details**.
2. Click **Create** to create the entity.
3. Enter value **emailid**.
4. Switch synonyms to patterns, and add this regular expression <b>^[a-zA-Z0-9.!#$%&’*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$</b> to identify emails.
5. When you are done adding, click the arrow to save and go back.

![](https://github.com/Deemaalamer/Dentist-Appointment-Booking-Bot/blob/master/images/bot5.gif)

6. Add your second entity and call it **@reason_for_visit**.
7. Click **Create** to create the entity.

![](https://github.com/Deemaalamer/Dentist-Appointment-Booking-Bot/blob/master/images/bot6.gif)

8. Add values such as: filling, gum problem, tooth cleaning, toothache etc. Also don't forget to add synonyms.

![](https://github.com/Deemaalamer/Dentist-Appointment-Booking-Bot/blob/master/images/bot7.PNG)

9. Under **System entities**, turn **@sys-time, @sys-date and @sys-number** on. This will allow the bot to detect dates, time and numbers.

![](https://github.com/Deemaalamer/Dentist-Appointment-Booking-Bot/blob/master/images/bot8.gif)

## Task 5.1: Build the dialog
A dialog is made up of nodes that define steps in the conversation.

1. Click on dialog tab, then Click on **Create** to create twi default nodes.

![](https://github.com/Deemaalamer/Dentist-Appointment-Booking-Bot/blob/master/images/bot9.gif)

In the previous image, two dialog nodes are created. The first node is the standard welcome
message. The other node is a catch-all node named "Anything else." Dialog nodes are chained in
a tree structure to create an interactive conversation with the user. The evaluation starts at the
top, so the welcome node is assessed before the "Anything else" node.

2. Click the welcome node to edit it. This node starts as soon as when the user initiates a conversation with the bot.
3. In the Welcome node, click on **Customize** in the top right corner.
4. Turn **Multiple responses** on, then click **Apply**.

![](https://github.com/Deemaalamer/Dentist-Appointment-Booking-Bot/blob/master/images/bot10.gif)

5. Now you're going to make your bot detect what time of the day it is and welcome the user accordingly.
**now().before('12:00:00')** detects if the conversation is in the morning and triggers good
morning. **now().before('16:00:00')** detects if the conversation is in the evening and triggers good
afternoon. **now().before('24:00:00')** detects if the conversation is in the evening and triggers good
evening. So now, for the first slot you can welcome the user by saying 'Good morning & welcome to ABC Dental Clinic. How can I help you?'. For the second slot, you can change it to good afternoon instead. For the last slot, change it to good evening.

![](https://github.com/Deemaalamer/Dentist-Appointment-Booking-Bot/blob/master/images/bot11.PNG)

## Task 5.2: Build the dialog

1. Add your second node below the 'Welcome' node, and call it 'Book dental appointment'.
2. Edit condition to *if bot recognizes*: **#book_appointment**.
3. In the Book dental appointment node, click on **Customize** in the top right corner.
4. Turn **Slots** on, then click **Apply**.

![](https://github.com/Deemaalamer/Dentist-Appointment-Booking-Bot/blob/master/images/bot12.gif)

5. In the first slot add check for **@sys-date** save as **$appointmentDate**, if not present, ask **Please enter preferred appointment date**
6. In the second slot add check for **@sys-time** save as **$appointmentTime**, if not present, ask **Please enter preferred appointment time**
7. In the third slot add check for **@reason_for_visit** save as **$reasonForVisit**, if not present, ask **Please enter reason for appointment/visit**
8. In the fourth slot add check for **@sys-number** save as **$mobileNumber**, if not present, ask **Please enter valid mobile number!**
9. In the fifth slot add check for **@personal_details:emailid** save as **$emailid**, if not present, ask **Please enter your email id**

![](https://github.com/Deemaalamer/Dentist-Appointment-Booking-Bot/blob/master/images/bot13.PNG)

10. Then in the next section add this as the reponse, '**Thank you! Your appointment has been booked for $appointmentDate $appointmentTime with Dr.XYZ. If you have any concerns please reach out to ABC Dental Clinic contact number. Have a good day! :)**'
 
![](https://github.com/Deemaalamer/Dentist-Appointment-Booking-Bot/blob/master/images/bot14.PNG)

## Task 5.3: Build the dialog

1. Add your third node below the 'dental appointment' node, and call it 'Thank you'. This node is used to responded to user when he/she is thankful.
2. Edit condition to *if bot recognizes*: **#thanks**
3. Add multiple response, such as: You're welcome, my pleasure, anytime, you're looking forward to your appointment.. etc

![](https://github.com/Deemaalamer/Dentist-Appointment-Booking-Bot/blob/master/images/bot15.gif)

## Task 6: Train and test your bot

1. Navigate to the '**Try it**' button at the top left corner of the page.
2. Start typing away to book an appointment and see how your bot responds!

You may even incorporate more details and improve the bot, the floor is yours.

![](https://github.com/Deemaalamer/Dentist-Appointment-Booking-Bot/blob/master/images/bot16.gif)


## Optional Task: Link the service to a UI

1. If you don't have Install Nodejs http://blog.teamtreehouse.com/install-node-js-npm-windows
2. **"Clone or Download** [Basic Conversation](https://github.com/lccmachado/Basic-Conversation) \repository.
3. Take note of Watson Conversation Service's **Credentials** and **workspace id**
4. Edit the file **app.js** and fill the fields **username**, **password** and **workspace_id** with the data
collected in the last step.
5. Open a terminal/console and change the directory where you downloaded your code.
6. Run the code by typeing **node app.js** in the command line.
7. Navagite to the **http://localhost:3000/** in your broswer to view and test your application

![](https://github.com/Deemaalamer/Dentist-Appointment-Booking-Bot/blob/master/images/bot17.png)

## Summary

You completed the tutorial. **Congratulations!**

In this tutorial, you completed these tasks:

1. Created a Watson conversation service.
2. Created a workspace
3. Created intents and entities
4. Built a dialog
5. Trained and tested a cognitive chatbot
6. Linked your trained bot to a UI

This tutorial scratches the surface of many of the capabilities of IBM Watson Conversation.

## Contributors

Thanks goes to these wonderful people:

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore -->
| [<img src="https://avatars2.githubusercontent.com/u/9212117?s=400&u=e8e8f322cb3d83a5442fe372c64884b7ffa1ee3c&v=4" width="100px;"/><br /><sub><b>Deema Alamer</b></sub>](https://twitter.com/deemaalamer)<br />[💻](#Contributors "Code") [📖](#Contributors "Documentation") | [<img src="https://avatars3.githubusercontent.com/u/31738704?s=400&v=4" width="100px;"/><br /><sub><b>Nailah ALTayyar</b></sub>](https://twitter.com/naila_musaid)<br />[📖](#Contributors "Documentation")
| :---: | :---: |

This project follows the [all-contributors][all-contributors] specification.
Contributions of any kind are welcome!

[all-contributors]: https://github.com/kentcdodds/all-contributors

## Acknowledgement

The **Dentist Appointment Booking Bot** was orginally created by Riya Roy and published on [Bot Asset Exchange](https://developer.ibm.com/code/exchanges/bots/category/healthfitness)
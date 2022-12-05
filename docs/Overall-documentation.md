# Documentation of Room Control System

The aim of this text is to provide the documentation regarding the architecture of room control system designed by Charles University Master’s students for the course Architecture of Software Engineering in winter 2022.

## Purporse
The purpose of the system is to modernize the hospital and make the patients' stay as comfortable as possible. At the same time, we want to give the hospital staff an easy way to monitor the rooms they are assigned to.
For example, the functionalities of our system include, but are not limited to:
- checking and setting the room temperature
- opening and closing the windows
- calling a nurse to the patient's room

## Stakeholders 

Patients, hospital staff and hospital management represent the stakeholders, since the system enables an easier operation of the hospital for patients as well as staff. Moreover, it minimizes cost of the development. 

## Concerns 

The application has to be easy to learn, since the staff training would be an additional cost. 

## Containers
The system consists of multiple containers. Some of which are part of the business logic. 

https://static.structurizr.com/workspace/78797/diagrams#RoomControl-Container.png
- External modules  
     __Log-in__: we assume that when an user logs into the system, this module will provide a token that contains the identification of the user. This token will be passed along with each request to the API.  
     __Equipment database (EDB)__: the assignment states that we can assume there is a hospital wide database with all the equipment of the hospital in it.


- User Interface

    The container User interface is an interface which is presented to users. It represents a web or mobile aplication or a remote controller. We expect the UI to remember an identification token for the user that is currently logged in. This token is passed along each request to the API.
- API

     The aim of the api is to provide access to the rooms network. It does not need to be configured for any specific UI so any type of it can use the same API. It receives requests from the UI along with the requests' parameters and makes appropriate calls to the controller of the business logic.
- Controller

    Controller is a part of business logic. It processes requests from the API. More precisely, this module decides which other modules should be called and then returns the results back to the API.
- Rooms

    The container rooms provides information regarding each room. For example, people assigned to the room as well as the equipment placed in the room.
- Notification

    The aim of the Notification module is to send notification from one instance of the UI to another. It is utilized for nurse call.
- Unified Equipment Interface
    
    Unified Equipment Interface provides a singular unified way of communicationg with each peace of equipment regardless of the manufacturer. It forwards requests as well as parameters to actual equipment through database communication module.
- Database Communication

    Communicates with the database and translates business logic calls into queries of the database needed.

## Side notes
- The module log-in was first a part of our business logic, but then we decided to leave it out and treat it as a separate system that we won't develop. This is because maybe it would be better to have one log-in service for all systems of the hospital, not only for room control. This would be up for discussion with the stakeholders.
- We originally had a module named people in our system, which would provide information about all registered users. This module would communicate with the log-in module when an user tries to log in. We then realized that the only thing we need to know about the users in our system is which room they are assigned to and whether or not they are part of the hospital staff. This module would seem redundant in this regard so we removed it.
- Information about the room the user is assigned to is now stored in the identification token of each user and passed along with each request. We then only verify it using the module Rooms.

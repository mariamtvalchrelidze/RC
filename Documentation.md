# Documentation of Room Control System

The aim of this text is to provide the documentation regarding the architecture of room control system designed by Charles University Master’s students for the course Architecture of Software Engineering in winter 2022.

## Purporse
The porpose of RC system is to allow users (patients as well as hospital staff) to monitor and control rooms in the hospital. 
By monitoring and controlling we mean: 
- checking and setting room temperature
- opening and closing windows
- calling a nurse 

### Stakeholders 

Patients, hospital staff and hospital management represent the stakeholders, since the system enables an easier operation of the hospital for patients as well as staff. Moreover, it minimizes cost of the development. 

### Concerns 

The application has to be easy to learn, since the staff training would be an additional cost. 

### Containers
The system consists of multiple containers. Some of which are part of the business logic. 


- User Interface

    The container User interface is an interface which is presented to users. It represents a web- or mobile aplication or a remote controller.
- API

     The aim of the api is to provide access to the rooms network. It does not need to be configured for any specific UI so any type of it can use the same API.
- Rooms

    The container rooms contains information regarding each room. For example, people assigned to the room as well as the equipment placed in the room.
- Controller

    Controller is a part of business logic. It processes requests from the API. More precisely, this module decides which modules to call and then returns the results back to the API.
- Notification

    The aim of the Notification module is to send notification from one instance of the application to another. It is utilized for nurse call.
- Unified Equipment Interface
    
    Unified Equipment Interface provides a singular unified way of communicationg with each peace of equipment regardless of the manufacturer. It forwards requests as well as parameters to actual equipment through database communication module.
- Database Communication

    Communicates with the database and translates business logic calls into queries of the database needed.



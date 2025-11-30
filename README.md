       APILedConnectivity 
<h1> Implemented API Led Connectivity through Mulesoft </h1>
<h3> Description </h3>
  This project demonstrates API-Led Connectivity in MuleSoft using System, Process, and Experience APIs with CRUD operations by using RAML(RESTful API Modeling Language) between two database tables.

<h3> Project Overview </h3>

  1. System API – Directly interacts with the database to perform CRUD operations.
  
  2. Process API – Fetches data from multiple System APIs, applies business logic, and prepares data for consumption.

  3. Experience API – Exposes clean, consumer-friendly endpoints for front-end applications.
  
<h3> Technologies used: </h3>
  <b> 1.Anypoint Platform (4.x): </b>
  
      Design Center - To design the API's with RAML
      
      Exchange - To store, share, and discover reusable API's
      
      Anypoint studio - To develop the API's
      
      Runtime Manager - To deploy the API's
      
  <b> 2.MySQL Database: </b>   
  
      create 2 tables
      
      empdetails - to store employee work details
      
      emppersonal - to store employee personal details
      
<h3> Project Structure </h3>

  endpoint(url) -> experience API -> process API -> system API
  
  /employees – empdetails table (work details)
  
    Performs all CRUD operations. 
    
    For delete, instead of removing the record, the status is updated to “terminated” (soft delete).
    
  /empPersonal – emppersonal table (personal details)
  
    Supports post, get, and put operations only. 
    
    For post, a scheduler in the Process API adds records at a specified time.
    
    While fetching details, both personal and work information should be merged and displayed to the user. This is handled using DataWeave code in the Process API.
    
  <b> Experience API: </b>
  
      endpoints:-
      
        post: /employees
        
        get: /employees
        
        put: /employees - id as query parameter
        
        delete: /employees - id as query parameter
        
        put: /empPersonal - id as query parameter
        
  <b> Process API: </b>
  
      endpoints:-
      
        post: /employees
        
        get: /employees
        
        put: /employees - id as query parameter
        
        delete: /employees - id as query parameter
        
        put: /empPersonal - id as query parameter
        
  <b> System API: </b>
  
      endpoints:-
      
        post: /employees
        
        get: /employees
        
        put: /employees - id as query parameter
        
        delete: /employees - id as query parameter
        
        post: /empPersonal
        
        get: /empPersonal
        
        put: /empPersonal - id as query parameter    
        
<h3> Features: </h3> 
  Layered API architecture (System → Process → Experience) 
  
  CRUD operations on relational database tables in System API 
  
  Business logic for merging and scheduler implementation in Process API  
  
  Consumer-friendly JSON response through Experience API
  
  Fully documented with RAML 1.0
  
<h3> API Architecture Diagram </h3>

          ┌───────────────────┐
          │  Experience API   │
          │ (Consumer Layer)  │
          └────────┬──────────┘
                   │
                   ▼
          ┌───────────────────┐
          │   Process API     │
          │ (Business Logic)  │
          │ - Merges personal │
          │   and work data   │
          │ - Scheduler adds  │
          │   records         │
          └────────┬──────────┘
                   │
                   ▼
          ┌───────────────────┐
          │   System APIs     │
          │ (Data Access)     │
          │ - /employees      │
          │ - /empPersonal    │
          └────────┬──────────┘
                   │
                   ▼
             ┌──────────┐
             │ Database │
             └──────────┘

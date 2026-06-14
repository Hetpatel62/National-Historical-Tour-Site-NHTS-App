NATIONAL HISTORICAL TOUR SITE (NHTS) — Agile SDLC Design Project
================================================================================

Project Type   : Software Design & Requirements Engineering
Team           : Group 11
Members        : Het Patel, Paul Bahiga, Karanpreet Kaur, Eric Thai
Methodology    : Agile / SDLC
Course         : ACS-2913-002 — Software Requirements Analysis and Design


--------------------------------------------------------------------------------
PROJECT OVERVIEW
--------------------------------------------------------------------------------

This project covers the full Agile SDLC design for the National Historical Tour
Site (NHTS) — a mobile/web application that enables tourists to explore
historical sites through Augmented Reality (AR) tour experiences. Tour guides
can create and manage AR tour groups, while users can register accounts and
access interactive historical content from any location.

The system supports two primary use cases:
  1. Create User Account  — Users register by entering personal information;
                            the system validates input and assigns a unique
                            account number granting access to app features.
  2. Create AR Tour Group — Tour guides create AR-enabled tour groups with
                            unique group IDs, allowing tourists to join and
                            experience historical sites interactively.


--------------------------------------------------------------------------------
ARTIFACTS PRODUCED
--------------------------------------------------------------------------------

Q1 — Agile Use Case Descriptions
  - Use Case: Create User Account
      Actors       : Tourist/User, Customer Representative, Site Guides
      Stakeholders : Tourists (External), Customer Representatives and
                     Site Guides (Operational)
      Includes     : Pre-conditions, post-conditions, main flow of events,
                     exception conditions (invalid input, duplicate accounts,
                     technical failures)

  - Use Case: Create AR Tour Group
      Actors       : Tour Guides, Visitors/Tourists
      Stakeholders : Tour Guides (Operational), Visitors (External)
      Related UCs  : Join AR Tour Group, Manage AR Tour Content
      Includes     : Pre-conditions, post-conditions, main flow of events,
                     exception conditions (technical issues, security concerns)

Q2 — Agile Activity Diagrams
  - Activity diagram for AR Tour Group Creation
      (swimlane: User | System)
      Flow: login/signup → AR group creation → group name validation →
            group ID generation → security check → app visitors
  - Activity diagram for User Account Creation
      (swimlane: User | System)
      Flow: app access → account creation → information prompt →
            validation loop → unique ID generation → home page

Q3 — Agile System Sequence Diagrams (SSD)
  - SSD for Create User Account
      Key messages: accessNHTSApp, selectCreateAccount,
                    provideInformation(Name, Address, PhoneNumber, EmailAddress),
                    validateInformation [loop: not valid → update],
                    generateUniqueAccountNumber, allowAccessToFeatures
  - SSD for Create AR Tour Group
      Key messages: launchApplication, selectARGroupCreation,
                    enterGroupName(name), validateGroupName [loop: not valid],
                    generatesUniqueGroupID, enterGroupID, activatedGroup

Q4 — Agile First Cut Design Class Diagram
  Controller : ARTourGuide (<<Controller>>)
  Classes    : Customer, HistoricalSite, NavigationGuide, AR_Elements,
               Images, audioGuide, videos, UserFeedback, Rating
  Key relationships:
    Customer → HistoricalSite
    HistoricalSite → NavigationGuide
    NavigationGuide → AR_Elements, UserFeedback
    AR_Elements → Images, audioGuide, videos
    UserFeedback → Rating

Q5 — Agile CRC Cards & Sequence/Communication Diagrams
  CRC Cards:
    - TourGroupHandler    : createTourGroup      → TourGroup
    - TourGroup           : createGroupMember    → GroupMember
    - GroupMember         : addUsers/removeUsers → UserDB
    - ProductHandler      : createNewProduct     → Product
    - Product             : createProductInfo, addToInventory → ProductInfo, Inventory
    - ProductInfo         : collectProductInfo   → ProductDB
    - UserHandler         : createUser, createAccount, createAddress → User
    - User                : createAccount, createAddress → Account, Address
    - Account             : updateUserInformation → AccountDB
    - Address             : updateUserAddress    → AddressDB

  Communication Diagram:
    - Create New Tour Group: User → TourGroupHandler → TourGroup → Admin
    - Create New Product:    Salesman → productHandler → Product → ProductInfo

  Sequence Diagram:
    - Create AR Tour Group: Actor → UserWindow → TourGroupHandler →
                            User → TourGroup → UserDA → GroupMember

Q6 — Agile Fully Developed Design Class Diagram
  Full system diagram including methods:
    Classes  : ARTourGuide (Controller), Customer, HistoricalSite,
               NavigationGuide, AR_Elements, Images, audioGuide,
               videos, UserFeedback, Rating
  Key methods:
    Customer        : createCustomer(ID,status,name,address), updateStatus(status)
    HistoricalSite  : createSite(ID,Name,Location,Desc,hours,rating)
    NavigationGuide : createNavigationGuide(...), updateNavType(), changeTourDate(date)
    AR_Elements     : createNewElement(id,name), setElementId(id), setElementName(name)
    Images          : createImage(id,name,desc)
    audioGuide      : createAudioGuide(id,name,desc)
    videos          : createVideo(id,name,desc)
    UserFeedback    : addFeedback(id,customer,desc,date), editFeedback(description)
    Rating          : newRating(id,customer,rating), editRating(rating)

Q7 — Agile Class Package Diagram
  2-layer architecture:
    View Layer   : NavigationGuide, HistoricalSite, AR_Elements,
                   Product, TourGroup, User
    Domain Layer : Customer, UserFeedback, Rating, ProductHandler,
                   TourGroupHandler, UserHandler, Address, Account


--------------------------------------------------------------------------------
KEY SYSTEM FEATURES
--------------------------------------------------------------------------------

- User registration with input validation and unique account number generation
- AR tour group creation with unique group ID and name uniqueness validation
- Multi-actor system supporting tourists, tour guides, and customer reps
- Augmented reality content delivery via Images, Audio Guides, and Videos
- User feedback and rating system for historical sites
- Navigation guide with tour date management and navigation type controls
- Product management for tour-related merchandise (salesman flow)
- Exception handling for invalid input, duplicate accounts, and technical issues
- Security and privacy controls for AR tour group settings


--------------------------------------------------------------------------------
TECH CONTEXT / DESIGN DECISIONS
--------------------------------------------------------------------------------

- MVC pattern applied: ARTourGuide acts as Controller
- AR_Elements serves as the base class for multimedia content (Images,
  audioGuide, videos) — enables extensible content delivery
- NavigationGuide links Customer to HistoricalSite, supporting location-aware
  tour routing
- CRC card design separates handlers (TourGroupHandler, ProductHandler,
  UserHandler) from domain entities for clean responsibility assignment
- 2-layer package architecture separates View presentation from Domain logic


--------------------------------------------------------------------------------
SKILLS DEMONSTRATED
--------------------------------------------------------------------------------

- Requirements elicitation and Agile use case documentation
- Multi-actor stakeholder analysis (tourists, guides, customer reps)
- Process flow modeling (activity diagrams, SSDs with loop fragments)
- Agile artifact creation (CRC cards, communication and sequence diagrams)
- Object-oriented design (first cut and fully developed class diagrams)
- Class package architecture with layered separation of concerns
- AR and location-based system design thinking
- SDLC end-to-end coverage from requirements to detailed design


--------------------------------------------------------------------------------

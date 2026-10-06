# Ticket-Booking-Project

## Overview

This project aims to design and evaluate an efficient train ticket booking system that provides seamless reservation and seat management capabilities to users. The system implements a comprehensive approach to handling user authentication, train search, real-time seat availability, and booking management.

## SCOPE AND OBJECTIVES

An effective solution to the issue of seat management and reservation handling in transportation systems is the Train Ticket Booking System. This application provides users with accurate and reliable train ticket booking technology.

### OBJECTIVES

- Investigate and assess existing user authentication and profile management systems
- Design a dynamic user profiling system that adapts to user preferences and booking history
- Create a train ticket booking system that utilizes multiple service-oriented components
- Implement efficient seat allocation and availability tracking mechanisms
- Utilize appropriate algorithms to ensure booking accuracy and prevent double-booking
- Evaluate system performance in handling concurrent user sessions and transactions
- Develop secure password management using industry-standard encryption techniques

## DESCRIPTION OF PROPOSED SYSTEM

The application is developed using an object-oriented and service-oriented architecture, composed of four primary increments:

1. **Presentation Layer (UI)** - Command-line interface for user interaction
2. **Service Layer** - Business logic for bookings, train search, and user management
3. **Entity Layer** - Data models for Train, User, and Ticket entities
4. **Persistence Layer** - JSON-based file storage for data management

The requirements are decomposed into manageable modules following the incremental development methodology.

## DATASET DESCRIPTION

The system operates with three primary data sources:

### 1. **Trains Dataset**
Contains comprehensive train information:
- **Train ID**: Unique identifier for each train
- **Train Number**: Official railway identification number
- **Station Information**: List of stations in route sequence with arrival/departure times
- **Seat Availability**: 2D matrix representation of seat occupancy (0 = available, 1 = booked)
- **Route Information**: Stations and time mappings for journey tracking

### 2. **Users Dataset**
Stores registered user profile information:
- **User ID**: Unique identifier (UUID format)
- **Username**: User login credential
- **Password**: Plain text password for session validation
- **Hashed Password**: Bcrypt-encrypted password for secure storage
- **Booking History**: List of tickets/reservations under user account
- **Location**: User's geographical location (for future filtering)

### 3. **Ratings/Bookings Dataset**
Maintains booking transaction records:
- **Booking ID/Ticket ID**: Unique booking reference
- **User ID**: Associated user account
- **Train ID**: Booked train identifier
- **Seat Details**: Row and column of reserved seat
- **Booking Timestamp**: Date and time of reservation
- **Booking Status**: Active, Cancelled, or Completed

## PROJECT STRUCTURE
ticket-booking-project/ ├── app/ │ ├── src/ │ │ ├── main/ │ │ │ └── java/org/example/ │ │ │ ├── App.java # Main CLI application entry point │ │ │ ├── entities/ │ │ │ │ ├── Train.java # Train model with seat matrix │ │ │ │ ├── User.java # User account model │ │ │ │ └── Ticket.java # Booking/Ticket model │ │ │ ├── services/ │ │ │ │ ├── UserBookingService.java # User & booking orchestration │ │ │ │ └── TrainService.java # Train search & seat management │ │ │ ├── util/ │ │ │ │ └── UserServiceUtil.java # Password hashing utilities │ │ │ └── localDb/ │ │ │ ├── users.json # Persistent user storage │ │ │ └── trains.json # Persistent train storage │ │ └── test/ │ │ └── java/org/example/ │ │ └── AppTest.java # Unit test suite │ └── build.gradle # Gradle build configuration ├── settings.gradle # Multi-project configuration ├── gradlew / gradlew.bat # Gradle wrapper scripts └── README.md # Documentation

## TECHNOLOGY STACK

- **Language**: Java 8
- **Build System**: Gradle 8.10
- **Testing Framework**: JUnit
- **Data Serialization**: Jackson (JSON processing)
- **Security**: jBCrypt 0.4 (Password hashing)
- **Storage**: JSON file-based persistence
- **Utilities**: Google Guava

### Dependencies

```gradle
- com.fasterxml.jackson.core:jackson-databind:2.13.4.2
- org.mindrot:jbcrypt:0.4
- com.google.guava:guava
- junit (for testing)
SYSTEM ARCHITECTURE
Layered Architecture
1. Entity Layer
Defines the core data models:

Train: Represents train information, routes, and seat inventory
User: Represents user accounts with authentication credentials
Ticket: Represents booking confirmations and reservations
2. Service Layer
Implements business logic and operations:

UserBookingService

User registration (sign-up with password hashing)
User authentication (login with credential validation)
Booking operations (book, cancel, view tickets)
Train search orchestration
Seat availability queries
TrainService

Train search by source-destination route
Seat availability management
Train data persistence (add/update operations)
Route validation logic
3. Utility Layer
Provides helper functions:

Password hashing using BCrypt
Password verification and validation
Data transformation and validation
4. Persistence Layer
Manages data storage and retrieval:

Jackson ObjectMapper for JSON serialization
File-based storage operations
In-memory data caching
Atomic write operations
BOOKING SYSTEM APPROACHES
The Train Ticket Booking System implements multiple algorithmic approaches:

1. Authentication Approach
BCrypt-based Password Hashing: Industry-standard encryption for credential security
User Profile Caching: In-memory user data for fast session validation
Stream-based User Lookup: Efficient filtering through user collections
2. Train Search Approach
Route-based Filtering: Validates trains operate on requested route
Station Sequence Validation: Ensures source comes before destination
List Filtering Algorithm: Linear search with custom predicates
3. Seat Booking Approach
Matrix-based Availability Tracking: 2D array representation of seat status
Atomic Booking Operations: Prevents race conditions in single-threaded execution
Validation-first Strategy: Validates seat existence and availability before booking
4. Hybrid User Management
Stateful Session Management: Tracks active user throughout session
Profile Persistence: Maintains booking history across sessions
Dynamic Preference Tracking: Records user booking patterns
FEATURES
User Management
Sign Up: Create new account with encrypted password storage
Login: Authenticate existing users with BCrypt verification
Profile Management: Maintain user booking history and preferences
Session Handling: Track active user throughout application session
Train Operations
Search Functionality: Find trains by source and destination
Route Information: Display stations and timing details
Seat Visualization: Show seat availability in 2D grid format
Real-time Updates: Reflect current seat occupancy status
Booking Management
Seat Selection: Book specific seats by row and column
Booking Confirmation: Generate and store booking records
Booking Retrieval: View all user bookings and details
Cancellation: Cancel existing bookings and free seats
APPLICATION WORKFLOW
Code
START APPLICATION
    ↓
DISPLAY MAIN MENU
    ↓
USER CHOICE
    ├─→ SIGN UP: Collect credentials → Hash password → Store user
    ├─→ LOGIN: Validate credentials → Create session → Load booking history
    ├─→ SEARCH TRAINS: Get source/destination → Filter trains → Display results
    ├─→ BOOK SEAT: Select train → View seats → Update availability → Confirm booking
    ├─→ VIEW BOOKINGS: Load user tickets → Display all bookings
    ├─→ CANCEL BOOKING: Enter ticket ID → Remove from list → Free seat
    └─→ EXIT: End session
    ↓
REPEAT OR EXIT
USER INTERFACE
Menu-driven command-line interface:

Code
Running Train Booking System
Choose option:
1. Sign up
2. Login
3. Fetch Bookings
4. Search Trains
5. Book a Seat
6. Cancel my Booking
7. Exit the App
Seat Display Format
Code
Select a seat out of these seats:
0 0 0 0 0 0
0 0 1 0 0 0
0 0 0 0 0 0
0 0 0 0 0 0

(0 = Available, 1 = Booked)

Select the seat by typing the row and column
Enter the row: 
Enter the column:
GETTING STARTED
Prerequisites
Java 8 or higher
Gradle 8.10+ (or use bundled wrapper)
Git (for cloning repository)
Installation
Clone the repository:
bash
git clone https://github.com/Git4Prg/ticket-booking-project.git
cd ticket-booking-project
Build the project:
bash
./gradlew clean build
Run the application:
bash
./gradlew run
Running Tests
bash
./gradlew test
Build Configuration
Build variants and customization options:

bash
./gradlew build -x test        # Build without tests
./gradlew buildDependents      # Build dependencies
./gradlew --refresh-dependencies build  # Refresh and rebuild
USAGE EXAMPLE
Code
$ ./gradlew run

> Task :app:run
Running Train Booking System
Choose option
1. Sign up
2. Login
3. Fetch Bookings
4. Search Trains
5. Book a Seat
6. Cancel my Booking
7. Exit the App
1

Enter the username to signup
john_doe
Enter the password to signup
secure_password_123

---

Choose option
1. Sign up
2. Login
3. Fetch Bookings
4. Search Trains
5. Book a Seat
6. Cancel my Booking
7. Exit the App
4

Type your source station
bangalore
Type your destination station
delhi

1 Train id : TR001
station bangalore time: 14:00:00
station delhi time: 20:30:00

Select a train by typing 1,2,3...
1

5

Select a seat out of these seats
0 0 0 0 0 0
0 0 0 0 0 0
0 0 0 0 0 0
0 0 0 0 0 0

Select the seat by typing the row and column
Enter the row
1
Enter the column
2
Booking your seat....
Booked! Enjoy your journey
ALGORITHMS & METHODOLOGIES
1. Route Validation Algorithm
Code
For each train in trainList:
    Find sourceIndex in train.stations
    Find destinationIndex in train.stations
    If both found AND sourceIndex < destinationIndex:
        Add train to results
Return filtered results
2. Seat Booking Algorithm
Code
Input: train, row, column
1. Validate row index: 0 ≤ row < seats.size()
2. Validate column index: 0 ≤ column < seats[row].size()
3. Check seat status: seats[row][column] == 0 (available)
4. If available:
       Mark seat: seats[row][column] = 1
       Update train data
       Persist to JSON
       Return TRUE
5. Else:
       Return FALSE
3. User Authentication Algorithm
Code
Input: username, password
1. Get hashed password from database
2. Verify input password against hash using BCrypt
3. If verification succeeds:
       Create user session
       Load booking history
       Return authenticated user object
4. Else:
       Return authentication failure
4. Data Persistence Strategy
Code
On startup:
    Load users.json → deserialize to User objects → cache in memory
    Load trains.json → deserialize to Train objects → cache in memory

On modification:
    Update in-memory objects
    Serialize to JSON
    Write atomically to file

On shutdown:
    Persist all in-memory state to files
PERFORMANCE ANALYSIS
Time Complexity
Operation	Complexity	Notes
User login	O(n)	Linear search through users
Train search	O(n)	Filter through all trains
Seat booking	O(1)	Direct array access
View bookings	O(1)	Direct user object access
Cancel booking	O(k)	k = number of user's bookings
Space Complexity
User data: O(n) where n = number of users
Train data: O(m × s) where m = trains, s = seats per train
Overall: O(n + m × s)

CONCLUSION
The Train Ticket Booking System successfully demonstrates:

Effective user authentication and secure credential management
Service-oriented architecture with clear separation of concerns
Efficient seat allocation and availability tracking
Real-time booking confirmation and state management
File-based persistence with object serialization
The system proves that combining multiple algorithmic approaches—route validation, matrix-based seat tracking, and BCrypt authentication—creates a robust booking platform. While the current JSON-based implementation suits educational purposes, production deployment would benefit from database integration and enhanced concurrency control.

The modular architecture enables seamless scaling to advanced features including payment processing, recommendation engines, and multi-tenant support. The clear separation between service, entity, and utility layers ensures maintainability and testability for future enhancements.


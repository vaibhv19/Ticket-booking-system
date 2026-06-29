# 🚂 IRCTC Train Ticket Booking System

A **Command-Line Interface (CLI)** based Train Ticket Booking System built with **Core Java**. This application simulates real-world railway ticket booking workflows including user management, train search, seat allocation, and booking management—all without external frameworks or databases.

Perfect for learning **OOP principles, JSON persistence, password hashing, and CLI application design** in Java.

---

## 🎯 Overview

The IRCTC Train Booking System is a feature-rich CLI application that allows users to:
- **Register and authenticate** with secure password hashing
- **Search for available trains** between stations
- **Book seats** with real-time availability tracking
- **View and manage bookings** seamlessly
- **Cancel bookings** when needed

All data is persisted in JSON files—no SQL database required, making it ideal for prototyping and learning.

---

## ✨ Key Features

| Feature | Description |
|---------|-------------|
| 👤 **User Management** | Sign up, login, and user authentication with bcrypt password hashing |
| 🚂 **Train Search** | Search available trains between source and destination stations |
| 🪑 **Seat Booking** | Interactive seat selection with availability validation |
| 📋 **Booking Management** | View all user bookings with ticket details |
| ❌ **Booking Cancellation** | Cancel tickets and free up seats |
| 💾 **JSON Persistence** | All data stored in JSON files (no external database) |
| ⚙️ **CLI Menu-Driven** | Intuitive command-line interface for easy navigation |

---

## 🛠️ Tech Stack

| Component | Technology |
|-----------|-----------|
| **Language** | Java 21 |
| **Build Tool** | Gradle 9.3.1 |
| **Data Format** | JSON |
| **JSON Processing** | Jackson (jackson-databind 2.13.4.2) |
| **Password Security** | jbcrypt 0.4 |
| **Annotations** | Lombok 1.18.22 |
| **Testing** | JUnit |
| **Core Concepts** | OOP, Collections Framework, Java Streams, File I/O |

---

## 📂 Project Structure

```
irctc/
├── app/
│   ├── src/main/java/ticket/booking/
│   │   ├── App.java                          # CLI Entry point & menu-driven interface
│   │   ├── entities/
│   │   │   ├── User.java                     # User entity with authentication info
│   │   │   ├── Train.java                    # Train entity with seats & stations
│   │   │   └── Ticket.java                   # Ticket entity for bookings
│   │   ├── service/
│   │   │   ├── TrainService.java             # Train operations (search, add, update)
│   │   │   └── UserBookingService.java       # User & booking management
│   │   └── util/
│   │       └── UserServiceUtil.java          # Utility methods (password hashing)
│   │
│   ├── src/main/resources/
│   │   └── localDB/
│   │       ├── trains.json                   # Train data storage
│   │       └── users.json                    # User data storage
│   │
│   ├── src/test/java/ticket/booking/
│   │   └── AppTest.java                      # Unit tests
│   │
│   └── build.gradle                          # Gradle build configuration
│
├── gradle/
│   ├── libs.versions.toml                    # Dependency version management
│   └── wrapper/
│
├── settings.gradle                           # Gradle settings
├── gradle.properties
├── gradlew & gradlew.bat                     # Gradle wrapper scripts
└── README.md                                 # This file
```

---

## 🚀 Getting Started

### Prerequisites

- **Java 21** or higher
- **Git** (optional, for cloning)

### Installation & Setup

#### 1. Clone the repository
```bash
git clone https://github.com/yourusername/irctc.git
cd irctc
```

#### 2. Build the project
```bash
./gradlew build
```
*On Windows:*
```bash
gradlew.bat build
```

#### 3. Run the application
```bash
./gradlew run
```
*On Windows:*
```bash
gradlew.bat run
```

---

## 📖 How to Use

Once the application starts, you'll see an interactive menu:

```
Choose option
1. Sign up
2. Login
3. Fetch Bookings
4. Search Trains
5. Book a Seat
6. Cancel my Booking
7. Exit the App
```

### Workflow Example

**Step 1: Sign Up**
- Enter a username and password
- System creates a new user account with a unique ID
- Password is securely hashed using bcrypt

**Step 2: Login**
- Enter your credentials
- System validates password against stored hash
- Access personalized booking features

**Step 3: Search Trains**
- Enter source and destination stations
- System finds all available trains between these stations
- View train details and available seats

**Step 4: Book a Seat**
- Select a train from search results
- Choose your seat (row and column format)
- Booking is confirmed and persisted

**Step 5: View Bookings**
- Fetch all your booked tickets
- View ticket details (ticket ID, train, route, date)

**Step 6: Cancel Booking**
- Select a ticket to cancel
- Seat is freed up for other users

---

## 🏗️ Architecture & Design Patterns

### Core Components

#### **App.java** - Entry Point
- Menu-driven CLI interface
- User interaction and input handling
- Option routing to appropriate services

#### **Entities** (Domain Models)
- **User**: Stores user credentials (name, password hash) and booked tickets
- **Train**: Contains train details (ID, number, seats, stations, timings)
- **Ticket**: Represents a booking (ticket ID, user, route, date, train reference)

#### **Services** (Business Logic)
- **TrainService**: 
  - Loads/saves train data from/to JSON
  - Searches trains by route (source → destination)
  - Validates station sequences
  - Updates seat availability
  
- **UserBookingService**:
  - Manages user signup and login
  - Handles booking creation and cancellation
  - Persists user data and tickets

#### **Utilities**
- **UserServiceUtil**: Password hashing and validation using bcrypt

### Design Principles Used
- **Separation of Concerns**: Business logic separated from UI and persistence
- **JSON Persistence**: File-based data storage with Jackson ObjectMapper
- **Stream API**: Functional programming for data filtering and searching
- **Builder Pattern**: Used in entity construction (Lombok @Builder)
- **Immutable Data**: Read-only access through getters, controlled mutations through setters

---

## 💾 Data Storage

### File Structure
```
app/
├── src/main/resources/localDB/
│   ├── trains.json     # Train inventory
│   └── users.json      # User accounts & bookings
```

### Sample trains.json
```json
[
  {
    "train_id": "TRN001",
    "train_no": "12345",
    "seats": [[0,0,0],[0,0,0],[0,1,1]],
    "station_times": {
      "delhi": "08:00",
      "agra": "12:00",
      "mumbai": "20:00"
    },
    "stations": ["delhi", "agra", "mumbai"]
  }
]
```

**Seat Encoding**: `0` = Available, `1` = Booked

### Sample users.json
```json
[
  {
    "name": "john_doe",
    "password": "john@123",
    "hashed_password": "$2a$10$...",
    "tickets_booked": [...],
    "user_id": "USR-12345"
  }
]
```

---

## 🧪 Testing

Run unit tests using Gradle:

```bash
./gradlew test
```

---

## 🔐 Security Features

- ✅ **Password Hashing**: Uses bcrypt (jbcrypt) for secure password storage
- ✅ **User Validation**: Credentials verified against hashed passwords
- ✅ **Unique User IDs**: UUID-based user identification
- ✅ **Data Persistence**: JSON files stored with proper file I/O handling

---

## 🎓 Learning Outcomes

This project demonstrates proficiency in:
- Core Java (OOP, Collections, Streams, File I/O)
- Build tools (Gradle)
- Design Patterns (Service layer, Repository pattern)
- JSON processing (Jackson)
- Security best practices (Password hashing)
- CLI application development
- Data persistence without external databases
- Unit testing

---

## 🚀 Future Enhancements

- [ ] Database integration (PostgreSQL/MySQL)
- [ ] REST API (Spring Boot)
- [ ] Web UI (HTML/CSS/JavaScript)
- [ ] Payment integration
- [ ] Email notifications
- [ ] Advanced seat filtering (window seats, aisle seats)
- [ ] Booking history with analytics
- [ ] Multi-language support

---

## 📝 License

This project is open source and available under the MIT License.

---

## 🤝 Contributing

Contributions are welcome! Feel free to fork this repository and submit pull requests.

---

## 📧 Contact

For questions or suggestions, please open an issue on GitHub.

---

## 📚 Additional Resources

- [Java Documentation](https://docs.oracle.com/javase/)
- [Gradle User Guide](https://docs.gradle.org/)
- [Jackson Documentation](https://github.com/FasterXML/jackson)
- [jbcrypt](https://www.mindrot.org/projects/jbcrypt/)

---

**Happy Coding! 🎉**

```bash id="clone"
git clone https://github.com/vaibhv19/Ticket-booking-system.git
cd Ticket-booking
```

### 2. Build the project (Gradle)

```bash id="build"
gradle build
```

### 3. Run the application

```bash id="run"
gradle run
```

---

## 💻 CLI Workflow

```bash id="workflow"
Welcome to Ticket Booking System

1. Register
2. Login
3. View Shows
4. Book Ticket
5. Exit

Enter your choice: 4

Select Show → Select Seat → Confirm Booking

Booking Successful ✅
```

---

## 🧠 Key Concepts Implemented

* Object-Oriented Design (Encapsulation, Abstraction)
* Separation of Concerns (Layered architecture)
* File-based persistence using JSON
* Data processing using Java Streams
* Efficient seat allocation and validation logic

---

## ⚡ Challenges Solved

* Preventing duplicate seat bookings through validation logic
* Managing application state without a database
* Structuring a scalable backend-like system in a CLI environment

---

## 🔮 Future Improvements

* 🌐 Convert to REST API using Spring Boot
* 🗄️ Replace JSON storage with MySQL/MongoDB
* 🔒 Add authentication with JWT
* ⚡ Implement concurrency handling for simultaneous bookings
* 🎯 Build a frontend (React)

---

## 👨‍💻 Author

**Vaibhav Gupta**
GitHub: https://github.com/vaibhv19

---

## ⭐ Support

If you found this project useful, consider giving it a ⭐ on GitHub!

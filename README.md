# airbnb-clone-project

This project is a simplified clone of the Airbnb platform. It allows users to register as hosts or guests, list properties, book accommodations, leave reviews, and make secure payments. The goal is to replicate the core features of Airbnb with a modern tech stack and clean backend architecture.

---

##  Project Goals

- Build a scalable backend system using Django and Django REST Framework
- Implement secure APIs with role-based access
- Support booking, payment, and review flows
- Use modern DevOps tools and CI/CD pipelines

---

##  Team Roles

- **Backend Developer**: Responsible for implementing API endpoints, database schemas, and business logic.
- **Database Administrator**: Manages database design, indexing, and optimizations.
- **DevOps Engineer**: Handles deployment, monitoring, and scaling of backend services.
- **QA Engineer**: Ensures backend functionalities are thoroughly tested and meet quality standards.

---

##  Technology Stack

- **Django**: A high-level Python web framework used for building the RESTful API.
- **Django REST Framework**: Provides tools for creating and managing RESTful APIs.
- **PostgreSQL**: A powerful relational database used for data storage.
- **GraphQL**: Allows for flexible and efficient querying of data.
- **Celery**: For handling asynchronous tasks such as sending notifications or processing payments.
- **Redis**: Used for caching and session management.
- **Docker**: Containerization tool for consistent development and deployment environments.
- **CI/CD Pipelines**: Automated pipelines for testing and deploying code changes.

---

##  Database Design

### 1. **Users**
Represents individuals who can either host properties or make bookings.

- `id` – Unique identifier  
- `name` – Full name of the user  
- `email` – User’s email (unique)  
- `password_hash` – Encrypted password  
- `role` – e.g., guest or host  

**Relationships:**
- A user can list multiple properties (as a host).
- A user can make multiple bookings (as a guest).
- A user can write multiple reviews.

---

### 2. **Properties**
Represents accommodations listed by hosts.

- `id` – Unique identifier  
- `user_id` – Foreign key (host who listed the property)  
- `title` – Property title  
- `description` – Detailed description  
- `price_per_night` – Cost per night  

**Relationships:**
- Each property is owned by one user.
- A property can have many bookings.
- A property can have many reviews.

---

### 3. **Bookings**
Represents reservations made by users for properties.

- `id` – Unique identifier  
- `user_id` – Foreign key (guest making the booking)  
- `property_id` – Foreign key (property being booked)  
- `start_date` – Check-in date  
- `end_date` – Check-out date  

**Relationships:**
- A booking is made by one user for one property.
- A booking may result in a payment.

---

### 4. **Reviews**
Represents feedback left by users after a stay.

- `id` – Unique identifier  
- `user_id` – Foreign key (author of the review)  
- `property_id` – Foreign key (property being reviewed)  
- `rating` – Score (e.g., 1 to 5)  
- `comment` – Text feedback  

**Relationships:**
- A user can leave multiple reviews.
- Each review is associated with one property.

---

### 5. **Payments**
Represents transactions for confirmed bookings.

- `id` – Unique identifier  
- `booking_id` – Foreign key (associated booking)  
- `amount` – Payment amount  
- `payment_method` – e.g., credit card, PayPal  
- `status` – e.g., pending, completed  

**Relationships:**
- Each payment is linked to one booking.

---

##  Feature Breakdown

###  User Management  
Users can sign up, log in, and manage their accounts securely. The system supports two roles: **guests** (who book properties) and **hosts** (who list properties), each with access to role-specific functionalities.

###  Property Management  
Hosts can create, update, and delete property listings, including photos, descriptions, and pricing. This allows them to manage accommodations and attract bookings.

###  Booking System  
Guests can browse properties, select available dates, and make bookings. The system ensures availability and prevents overlapping reservations.

###  Payment Integration  
Secure payments are processed for confirmed bookings using simulated or real payment gateways. This ensures a seamless and trustworthy transaction process.

###  Reviews and Ratings  
After their stay, guests can leave reviews and ratings for properties. This builds trust and helps users make informed decisions.

###  Search and Filters  
Users can filter properties by location, date, price, and other criteria. This helps them quickly find the most suitable accommodations.

---

##  API Security

###  Authentication  
Secure login using **JWT** or **OAuth** to verify user identity before accessing protected resources.

**Why it matters**: Prevents unauthorized access to user data and protected features.

###  Authorization  
Role-based access control (RBAC) ensures users can only perform actions appropriate to their roles.

**Why it matters**: Stops users from accessing or modifying other users’ data.

###  Input Validation & Sanitization  
All input is validated and sanitized to prevent **SQL injection**, **XSS**, and other attacks.

**Why it matters**: Protects the database and system from malicious data input.

###  Rate Limiting  
Limits the number of API requests per user/IP to prevent brute-force or spam attacks.

**Why it matters**: Prevents abuse and server overload.

###  HTTPS Encryption  
All communication between clients and server is encrypted using HTTPS.

**Why it matters**: Protects sensitive data like passwords and payment info during transmission.

###  Secure Payments  
If using real payment gateways (e.g., Stripe, PayPal), data is tokenized and never stored directly.

**Why it matters**: Ensures financial information stays protected and builds user trust.

---

##  CI/CD Pipeline

### Why CI/CD is Important
- **Automated Testing**: Ensures new code doesn’t break existing features.
- **Faster Deployment**: Enables frequent and reliable release of updates.
- **Improved Collaboration**: Developers get quick feedback on pull requests.
- **Consistency**: The same process is used across environments, reducing deployment errors.

---

### Tools We May Use

- **GitHub Actions**: Automates tasks like testing, linting, and deployment.
- **Docker**: Packages the app into containers to ensure consistency across environments.
- **Heroku / Vercel / Netlify**: Platforms for automated deployment.
- **Postman / Newman**: For running automated API tests in the CI pipeline.

---

### Typical Workflow

1. Developer pushes code to GitHub.  
2. GitHub Actions runs tests, linters, and build steps.  
3. If tests pass, the app is built and deployed via Docker or directly to cloud.  
4. Results and feedback appear directly in the pull request.

---

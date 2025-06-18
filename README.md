# airbnb-clone-project
#Team roles
Backend Developer: Responsible for implementing API endpoints, database schemas, and business logic.
Database Administrator: Manages database design, indexing, and optimizations.
DevOps Engineer: Handles deployment, monitoring, and scaling of the backend services.
QA Engineer: Ensures the backend functionalities are thoroughly tested and meet quality standards.
#Technology Stack
Django: A high-level Python web framework used for building the RESTful API.
Django REST Framework: Provides tools for creating and managing RESTful APIs.
PostgreSQL: A powerful relational database used for data storage.
GraphQL: Allows for flexible and efficient querying of data.
Celery: For handling asynchronous tasks such as sending notifications or processing payments.
Redis: Used for caching and session management.
Docker: Containerization tool for consistent development and deployment environments.
CI/CD Pipelines: Automated pipelines for testing and deploying code changes.
#Database Design
1. Users
Represents individuals who can either host properties or make bookings.

id – Unique identifier

name – Full name of the user

email – User’s email (unique)

password_hash – Encrypted password

role – e.g., guest or host

 Relationships:

A user can list multiple properties (as a host).

A user can make multiple bookings (as a guest).

A user can write multiple reviews.

2. Properties
Represents accommodations listed by hosts.

id – Unique identifier

user_id – Foreign key (host who listed the property)

title – Property title

description – Detailed description

price_per_night – Cost per night

 Relationships:

Each property is owned by one user.

A property can have many bookings.

A property can have many reviews.

3. Bookings
Represents reservations made by users for properties.

id – Unique identifier

user_id – Foreign key (guest making the booking)

property_id – Foreign key (property being booked)

start_date – Check-in date

end_date – Check-out date

 Relationships:

A booking is made by one user for one property.

A booking may result in a payment.

4. Reviews
Represents feedback left by users after a stay.

id – Unique identifier

user_id – Foreign key (author of the review)

property_id – Foreign key (property being reviewed)

rating – Score (e.g., 1 to 5)

comment – Text feedback

 Relationships:

A user can leave multiple reviews.

Each review is associated with one property.

5. Payments
Represents transactions for confirmed bookings.

id – Unique identifier

booking_id – Foreign key (associated booking)

amount – Payment amount

payment_method – e.g., credit card, PayPal

status – e.g., pending, completed

 Relationships:

Each payment is linked to one booking.

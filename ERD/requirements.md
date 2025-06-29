# Airbnb Clone – ER Diagram Requirements

This document defines the entities, attributes, relationships, and constraints for the Airbnb Clone database system based on the project specifications.

---

## Entities and Attributes

### 1. User
- `user_id` (UUID, Primary Key, Indexed)
- `first_name` (VARCHAR, NOT NULL)
- `last_name` (VARCHAR, NOT NULL)
- `email` (VARCHAR, UNIQUE, NOT NULL)
- `password_hash` (VARCHAR, NOT NULL)
- `phone_number` (VARCHAR, NULL)
- `role` (ENUM: guest, host, admin, NOT NULL)
- `created_at` (TIMESTAMP, DEFAULT CURRENT_TIMESTAMP)

### 2. Property
- `property_id` (UUID, Primary Key, Indexed)
- `host_id` (UUID, Foreign Key → User.user_id)
- `name` (VARCHAR, NOT NULL)
- `description` (TEXT, NOT NULL)
- `location` (VARCHAR, NOT NULL)
- `pricepernight` (DECIMAL, NOT NULL)
- `created_at` (TIMESTAMP, DEFAULT CURRENT_TIMESTAMP)
- `updated_at` (TIMESTAMP, ON UPDATE CURRENT_TIMESTAMP)

### 3. Booking
- `booking_id` (UUID, Primary Key, Indexed)
- `property_id` (UUID, Foreign Key → Property.property_id)
- `user_id` (UUID, Foreign Key → User.user_id)
- `start_date` (DATE, NOT NULL)
- `end_date` (DATE, NOT NULL)
- `total_price` (DECIMAL, NOT NULL)
- `status` (ENUM: pending, confirmed, canceled, NOT NULL)
- `created_at` (TIMESTAMP, DEFAULT CURRENT_TIMESTAMP)

### 4. Payment
- `payment_id` (UUID, Primary Key, Indexed)
- `booking_id` (UUID, Foreign Key → Booking.booking_id)
- `amount` (DECIMAL, NOT NULL)
- `payment_date` (TIMESTAMP, DEFAULT CURRENT_TIMESTAMP)
- `payment_method` (ENUM: credit_card, paypal, stripe, NOT NULL)

### 5. Review
- `review_id` (UUID, Primary Key, Indexed)
- `property_id` (UUID, Foreign Key → Property.property_id)
- `user_id` (UUID, Foreign Key → User.user_id)
- `rating` (INTEGER, NOT NULL, CHECK: rating between 1 and 5)
- `comment` (TEXT, NOT NULL)
- `created_at` (TIMESTAMP, DEFAULT CURRENT_TIMESTAMP)

### 6. Message
- `message_id` (UUID, Primary Key, Indexed)
- `sender_id` (UUID, Foreign Key → User.user_id)
- `recipient_id` (UUID, Foreign Key → User.user_id)
- `message_body` (TEXT, NOT NULL)
- `sent_at` (TIMESTAMP, DEFAULT CURRENT_TIMESTAMP)

---

## Relationships

- A **User** can **own** many Properties (1:N)
- A **User** can **make** many Bookings (1:N)
- A **Property** can **have** many Bookings (1:N)
- A **Booking** can **generate** one Payment (1:1)
- A **Booking** can **result in** one Review (0:1)
- A **Property** can **have** many Reviews (1:N)
- A **User** can **send** and **receive** many Messages (1:N in both directions)

---

## Constraints Summary

- Unique: `email` in `User`
- Not Null: All required fields
- Foreign Key References:
  - `host_id` → `User.user_id`
  - `property_id` → `Property.property_id`
  - `user_id` → `User.user_id`
  - `booking_id` → `Booking.booking_id`
  - `sender_id`, `recipient_id` → `User.user_id`
- ENUM Validations:
  - `User.role`: guest, host, admin
  - `Booking.status`: pending, confirmed, canceled
  - `Payment.payment_method`: credit_card, paypal, stripe
- CHECK Constraint:
  - `Review.rating` must be between 1 and 5

---

## Indexing

- All Primary Keys are automatically indexed.
- Additional indexes should be added on:
  - `User.email`
  - `Property.property_id`
  - `Booking.property_id`, `Booking.booking_id`
  - `Payment.booking_id`

---

## Notes

- All `UUID` values serve as unique identifiers.
- `created_at`, `updated_at`, and `payment_date` use default timestamps for data tracking.
- The diagram should show relationships with cardinalities (1:1, 1:N, etc.).
- Optional: Use arrows or labels like "owns", "books", "reviews" to indicate direction.

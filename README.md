# 🚀 Serverless Event RSVP Management System (AWS)

A serverless full-stack web application built on AWS that allows users to view events and submit RSVPs in real time.  
The system is designed using AWS Free Tier–eligible services, follows modern cloud-native best practices, and cleanly separates structured and high-velocity data.

---

## 🖼️ UI Examples

![UI Example 1](/assets/ui1.png)  
![UI Example 2](/assets/ui2.png)  
![UI Example 3](/assets/ui3.png)

---

## 📌 Features

- 📅 View upcoming events with full details
- 📝 Submit RSVPs (Yes / No)
- 📊 Real-time RSVP count tracking
- ⚡ Serverless backend (auto-scaling, no server management)
- 🌍 Globally distributed frontend via CDN
- 💰 Cost-optimized using AWS Free Tier

---

## 🏗️ Architecture Overview

This project follows a **serverless architecture**, meaning no traditional servers are managed manually.

### Architecture Diagram
![Architecture Diagram](/assets/full-stack-archi.png)

### High-Level Flow
1. User interacts with the frontend (HTML/CSS/JS).
2. Frontend calls backend APIs via HTTP.
3. API Gateway routes requests to AWS Lambda.
4. AWS Lambda:
   - Fetches event data from Amazon RDS (MySQL).
   - Stores and updates RSVP data in Amazon DynamoDB.
5. Static frontend is served via S3 + CloudFront.

---

## 🧩 Tech Stack

### Frontend
- **HTML**
- **CSS**
- **JavaScript**
- Hosted on **Amazon S3**
- Delivered globally via **Amazon CloudFront**

### Backend
- **AWS Lambda** (Node.js)
- **Amazon API Gateway** (HTTP API)

### Databases
- **Amazon RDS (MySQL)**:  Stores structured event data.
- **Amazon DynamoDB**: Stores RSVP responses and real-time counters using a single-table design.

### Security & Networking
- VPC-enabled AWS Lambda functions.
- Security Groups for database access.
- IAM roles with scoped permissions.
- CORS enabled for frontend–backend communication.

### Cost Management
- AWS Free Tier-focused.
- Budget alerts to avoid unexpected charges.
- RDS pause/hibernate strategy.

---

## 🗂️ Database Design

### RDS (MySQL)
#### `events` table:
| **Column**    | Description                |
|---------------|----------------------------|
| eventID (PK)  | Primary Key                |
| title         | Event title                |
| description   | Event description          |
| startAt       | Event start time           |
| venue         | Event venue                |
| bannerURL     | URL for the event banner   |
| createdAt     | Record creation timestamp  |

- Used for event listings and detail pages.

---

### DynamoDB (NoSQL)
#### `eventRSVPResponses` table:
| **PK (Partition Key)** | SK (Sort Key)         | Purpose                 |
|-------------------------|-----------------------|-------------------------|
| event#123              | respondent#user@email | Individual RSVPs        |
| event#123              | response#YES          | Aggregated count (YES)  |
| event#123              | response#NO           | Aggregated count (NO)   |

- **Atomic Updates:** Ensures data consistency and prevents race conditions using transactions.
- **High-Concurrency Writes:** Supports real-time RSVP updates.

---

## 🔌 API Endpoints

| **Method** | **Endpoint**       | **Description**           |
|------------|--------------------|---------------------------|
| GET        | `/events`          | Fetch all events          |
| GET        | `/event/{id}`      | Fetch event details       |
| GET        | `/stats/{id}`      | Fetch real-time RSVP stats|
| POST       | `/rsvp`            | Submit a new RSVP response|

#### Backend Logic
- Single AWS Lambda function handles routing.
- Path-based request handling to determine action.
- Environment variables for database configuration.
- DynamoDB `TransactWriteItems` ensures atomic RSVP updates.
- Duplicate RSVP checks implemented.
- Full CORS support for frontend-backend communication.

---

## 🌐 Frontend Hosting

- Static assets hosted in **Amazon S3**.
- Delivered globally via **Amazon CloudFront** for:
  - Low latency.
  - Global delivery with caching.
  - HTTPS support for secure communication.

---

## 🧠 Design Decisions

### Why Use RDS + DynamoDB?
1. **RDS**: Ideal for storing structured, relational event data.
2. **DynamoDB**: Optimized for high-volume, concurrent RSVP writes.

This separation provides:
- Improved performance.
- High scalability.
- Better cost efficiency.

---

## 🔮 Future Enhancements

Planned improvements to make this app production-ready:
- 🔐 Add User Authentication using **Amazon Cognito**.
- 👨‍💼 Create an Admin Dashboard for event management.
- ✏️ Enable RSVP updates & cancellations.
- 📧 Add email confirmations for RSVPs.
- 🚦 Implement API rate limiting & input validation.
- 📊 Introduce monitoring & alerts via **Amazon CloudWatch**.
- 🧪 Add automated testing (unit and integration tests).

---

## 📷 Demo

![Screenshot Example](#)  
(Add more screenshots or demo video link here.)

---

## 🧑‍💻 Author

**Vaibhav Sapaliya**  
Computer Engineering Student | Cloud & Backend Enthusiast

If you found this project helpful, feel free to ⭐ the repo!
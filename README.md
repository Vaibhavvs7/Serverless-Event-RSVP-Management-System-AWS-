# 🚀 Serverless Event RSVP Management System (AWS)

A serverless full-stack web application built on AWS that allows users to view events and submit RSVPs in real time.  
The system is designed using AWS Free Tier–eligible services, follows modern cloud-native best practices, and cleanly separates structured and high-velocity data.

---

📌 **Features**

- 📅 View upcoming events with full details
- 📝 Submit RSVPs (Yes / No)
- 📊 Real-time RSVP count tracking
- ⚡ Serverless backend (auto-scaling, no server management)
- 🌍 Globally distributed frontend via CDN
- 💰 Cost-optimized using AWS Free Tier

---

🏗️ **Architecture Overview**

This project follows a serverless architecture, meaning no traditional servers are managed manually.

<img src = 'assests/full-stack-archi'>

**High-level flow:**
1. User interacts with the frontend (HTML/CSS/JS)
2. Frontend calls backend APIs via HTTP
3. API Gateway routes requests to AWS Lambda
4. Lambda:
   - Fetches event data from MySQL (RDS)
   - Stores and updates RSVP data in DynamoDB
5. Static frontend is served via S3 + CloudFront

---

🧩 **Tech Stack**

**Frontend**
- HTML
- CSS
- JavaScript
- Hosted on Amazon S3
- Delivered globally via Amazon CloudFront

**Backend**
- AWS Lambda (Node.js)
- Amazon API Gateway (HTTP API)

**Databases**
- **Amazon RDS (MySQL)**:  Stores structured event data
- **Amazon DynamoDB**: Stores RSVP responses and real-time counters using a single-table design

**Security & Networking**
- VPC-enabled Lambda
- Security Groups for database access
- IAM roles with scoped permissions
- CORS enabled for frontend–backend communication

**Cost Management**
- AWS Free Tier focused
- Budget alerts to avoid unexpected charges
- RDS pause/hibernate strategy

---

🗂️ **Database Design**

**RDS (MySQL)**

| events table |
|--------------|
| **eventID (PK)** | title | description | startAt | venue | bannerURL | createdAt |

- Used for event listings and detail pages

**DynamoDB (NoSQL)**

| PK (Partition Key) | SK (Sort Key) | Purpose               |
|--------------------|---------------|-----------------------|
| event#123          | respondent#*user@email* | Individual RSVP         |
| event#123          | response#YES  | Aggregated YES count  |
| event#123          | response#NO   | Aggregated NO count   |

✔ Enables atomic updates  
✔ Supports high-concurrency writes  
✔ Prevents race conditions using transactions

---

🔌 **API Endpoints**

| Method | Endpoint         | Description          |
|--------|------------------|----------------------|
| GET    | /events          | Fetch all events    |
| GET    | /event/{id}      | Fetch event details |
| GET    | /stats/{id}      | Fetch RSVP stats    |
| POST   | /rsvp            | Submit an RSVP      |

**Backend Logic**
- Single Lambda function handles routing
- Path-based request handling
- Environment variables for DB configuration
- DynamoDB TransactWriteItems for atomic RSVP + counter updates
- Duplicate RSVP checks
- CORS support for frontend access

---

🌐 **Frontend Hosting**

- Static assets hosted in Amazon S3
- CloudFront CDN for low latency, global delivery, and HTTPS support

---

🧠 **Design Decisions**

- **Why RDS + DynamoDB?**
  - RDS → Structured, relational event data
  - DynamoDB → High-volume, concurrent RSVP writes
  - Improves performance, scalability, and cost efficiency

---

🔮 **Future Enhancements**

Planned improvements to make this production-ready:
- 🔐 User authentication (Amazon Cognito)
- 👨‍💼 Admin dashboard for event management
- ✏️ RSVP update & cancellation
- 📧 Email confirmations
- 🚦 API rate limiting & validation
- 📊 Monitoring & alarms (CloudWatch)
- 🧪 Automated tests

---

📷 **Demo**

(Add screenshots / demo video link here)

---

🧑‍💻 **Author**

**Vaibhav Sapaliya**  
Computer Engineering Student | Cloud & Backend Enthusiast

If you found this project helpful, feel free to ⭐ the repo!
